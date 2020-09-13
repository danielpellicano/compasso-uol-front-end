<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/img/uol-compasso.svg" width="500" />
    <FieldSearch />
    <ResultSearch />
  </div>
</template>

<script>
import FieldSearch from "./components/FieldSearch.vue";
import ResultSearch from "./components/ResultSearch.vue";

export default {
  name: "App",
  components: {
    FieldSearch,
    ResultSearch,
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
