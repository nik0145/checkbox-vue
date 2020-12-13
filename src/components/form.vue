<template>
  <div class="hello">
    <form class="review-form" @submit.prevent="onSubmit" v-if="checkboxes">
      <div v-for="(elem, i) in checkboxes" :key="i">
        <Checkbox
          :category="elem.category"
          @onCheckedElement="saveData"
          :value="elem.value"
        />
      </div>

      <p>
        <input type="submit" value="Сохранить" />
      </p>
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
        { category: "Овощи1", value: ["Огурцы1", "Морковь1", "Помидоры1"] },
        { category: "Овощи2", value: ["Огурцы2", "Морковь2", "Помидоры3"] },
      ],
    };
  },
  components: {
    Checkbox,
  },
  methods: {
    saveData(checkboxValue) {
      let {key ,value} = checkboxValue
      this.dataSubmut = [
        { category: key, checkedValues: value },
        ...this.dataSubmut.filter(item => item.category !==key),
      ];
    },
    onSubmit() {
      this.$emit('onShowForParent',this.dataSubmut)
    },
  },
};
</script>

<style scoped></style>
