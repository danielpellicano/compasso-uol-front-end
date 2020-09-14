<template>
  <div id="app" class="home">
    <img
      class="logo"
      alt="Uol Compasso"
      :src="require('../assets/img/uol-compasso.svg')"
      width="500"
    />
    <FieldSearch @search="apiSearch" @countSearch="countSearch" />
    <ResultSearch ref="resultSearch" :query="query" />
  </div>
</template>

<script>
import FieldSearch from "../components/FieldSearch.vue";
import ResultSearch from "../components/ResultSearch.vue";

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
    },
    countSearch(valor) {
      this.$refs.resultSearch.queryGitHub(this.$refs.resultSearch.query);
      this.count = valor.count;
    },
  },
};
</script>

<style>
body {
  padding: 0;
  margin: 0;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.logo {
  margin: 30px auto;
  display: block;
}
</style>
