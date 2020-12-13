<template>
  <div class="fl-row">
    <form class="review-form" @submit.prevent="onSubmit" v-if="checkboxes">
      <h2 class="w-250">Выбрать категорию</h2>
      <div class="fl-row">
        <div v-for="(elem, i) in checkboxes" :key="i">
          <Checkbox
            :category="elem.category"
            @onCheckedElement="saveData"
            :value="elem.value"
          />
        </div>
      </div>

      <div class="fl-content btn-wrap">
        <input
          :disabled="dataSubmut && dataSubmut.length === 0"
          type="submit"
          class="btn"
          value="Сохранить"
        />
      </div>
    </form>
  </div>
</template>

<script>
import Checkbox from "./checkbox.vue";

export default {
  name: "Form",
  data() {
    return {
      dataSubmut: [],
      checkboxes: [
        { category: "Овощи", value: ["Огурцы", "Морковь", "Помидоры"] },
        { category: "Фрукты", value: ["Бананы", "Яблоки", "Груши"] },
        { category: "Ягоды", value: ["Малина", "Клубника", "Черника"] },
      ],
    };
  },
  components: {
    Checkbox,
  },
  methods: {
    saveData(checkboxValue) {
      let { key, value } = checkboxValue;
      this.dataSubmut = [
        { category: key, checkedValues: value },
        ...this.dataSubmut.filter((item) => item.category !== key),
      ];
    },
    onSubmit() {
      this.$emit("onShowForParent", this.dataSubmut);
    },
  },
};
</script>

<style scoped>
.fl-content {
  display: flex;
  justify-content: flex-end;
}
.btn-wrap {
  margin: 10px;
}
.btn:disabled{
   
  background: #ccc;
}
.btn {
   border: none;
  color: white;
  padding: 15px 32px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  cursor: pointer;
  border-radius: 4px;
  background: #3f56e0;
  outline: none; 
}
.w-250 {
  width: 250px;
}
.fl-row {
  display: flex;
  flex-direction: row;
}
.fl-column {
  display: flex;
  flex-direction: column;
}
</style>
