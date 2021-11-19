<template>
  <div id="app">
    <AsyncJS />
  </div>
</template>

<script>
import AsyncJS from "./components/AsyncJS.vue";

export default {
  name: "App",
  components: {
    AsyncJS,
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
