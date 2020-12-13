<template>
  <div v-if="value && category">
    <ul>
      <li>
        <span>
          <label>
            <input
              type="checkbox"
              :indeterminate.prop="isIntermediate"
              v-model="isTrueMainCheckbox"
              id="checkall"
            />
            {{ category }} (выбрано {{ checked }} из {{ numberValue }})</label
          >
        </span>
      </li>
      <ul>
        <span v-for="(name, i) in value" :key="i">
          <li>
            <label>
              <input type="checkbox" :value="name" v-model="checkedNames" />
              {{ name }}</label
            >
          </li>
        </span>
      </ul>
    </ul>
  </div>
</template>

<script>
export default {
  name: "Checkbox",
  data() {
    return {
      checkedNames: [],
    };
  },
  watch: {
    checkedNames: function(value) {
      this.$emit("onCheckedElement", { key: this.category, value });
    },
  },
  computed: {
    checked: function() {
      return this.checkedNames.length;
    },
    numberValue: function() {
      return this.value.length || 0;
    },
    isIntermediate: function() {
      return (
        this.checkedNames.length < this.numberValue &&
        this.checkedNames.length !== this.numberValue &&
        this.checkedNames.length !== 0
      );
    },

    isTrueMainCheckbox: {
      get: function() {
        return this.checkedNames.length === this.numberValue;
      },
      set: function(newValue) {
        console.log(newValue);
        if (newValue === true) {
          this.checkedNames = [...this.value];
        } else {
          this.checkedNames = [];
        }
      },
    },
  },
  props: {
    category: String,
    value: Array,
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
ul {
  list-style: none;
  margin: 5px 20px;
}
label {
  margin-left: 5px;
}
li {
  margin: 10px 2px;
  text-align: left;
}
</style>
