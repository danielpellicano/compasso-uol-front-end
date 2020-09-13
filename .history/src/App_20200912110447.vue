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
  data() {
    return {
      msg: "GitHub Search",
      query: "",
      results: null,
    };
  },
  methods: {
    queryGitHub(q) {
      let self = this;
      fetch("https://api.github.com/users/" + q)
        .then((j) => {
          return j.json();
        })
        .then((r) => {
          console.log(r);
          self.results = r;
        });
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
