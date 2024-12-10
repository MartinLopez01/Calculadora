<template>
  <div id="app">
    <La_Calculadora />
  </div>
</template>

<script>
import La_Calculadora from "./components/La_Calculadora.vue";

export default {
  name: "App",
  components: {
    La_Calculadora,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
