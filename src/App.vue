<template>
  <div id="app">
    <Form @onShowForParent="showData" />
    <code v-if="data && data.length > 0">
      {{ data }}
    </code>
  </div>
</template>

<script>
import Form from "./components/form.vue";

export default {
  name: "App",
  data() {
    return {
      data: [],
    };
  },
  methods: {
    showData(value) {
      this.data = value;
    },
  },
  components: {
    Form,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
