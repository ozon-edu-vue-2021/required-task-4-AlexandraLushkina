<template>
  <div id="app">
    <Form />
  </div>
</template>

<script>
import Form from "./components/Form.vue";
export default {
  name: "App",
  components: {
    Form,
  },
};
</script>

<style>
#app {
  /* font-family: Avenir, Helvetica, Arial, sans-serif; */
  color: #2c3e50;
  background-color: #fafafa;
  padding: 24px;
  box-sizing: border-box;
  -webkit-text-fill-color: #001a34;
  border: 0;
  caret-color: #005bff;
  color: inherit;
  font-family: GTEestiPro, arial, sans-serif;
  font-size: 100%;
  line-height: 1.15;
  margin: 10px;
  outline: none;
  text-align: inherit;
  vertical-align: top;
  width: 100%;
}
html,
body,
#app {
  height: 100%;
}
* {
  box-sizing: border-box;
}
</style>

<style lang="scss">
@import "../node_modules/@braid/vue-formulate/themes/snow/snow.scss";
</style>
