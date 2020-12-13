<template>
  <div class="hello" v-if="value && category">
    <label
      ><input
        type="checkbox"
        :indeterminate.prop="isIntermediate"
        v-model="isTrue"
        id="checkall"
      />
      {{ category }}</label
    >
    <span v-for="(name, i) in value" :key="i">
      <input type="checkbox" :value="name" v-model="checkedNames" />
      <label>{{ name }}</label>
    </span>
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

    isTrue: {
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
<style scoped></style>
