<template>
  <div id="app">
    <img
      class="logo"
      alt="Uol Compasso"
      src="./assets/img/uol-compasso.svg"
      width="500"
    />
    <FieldSearch @search="apiSearch" @countSearch="countSearch" />
    <ResultSearch :query="query" :countSearch="count" />
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
  data() {
    return {
      query: "",
      count: 0,
    };
  },
  methods: {
    apiSearch(query) {
      this.query = query;
      console.log(query);
    },
    countSearch(valor) {
      this.count = valor;
    },
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
