<template>
  <div id="app" class="home">
    <div class="content">
      <img
        class="logo animate__animated animate__bounce"
        alt="Uol Compasso"
        :src="require('../assets/img/uol-compasso.svg')"
        width="500"
      />
      <FieldSearch @search="apiSearch" @countSearch="countSearch" />
      <ResultSearch ref="resultSearch" :query="query" :select="select" />
    </div>

    <footer>
      <p>© Teste para Front End Developer na Compasso Uol</p>
      <p>Desenvolvido por Daniel Pellicano</p>
    </footer>
  </div>
</template>

<script>
import FieldSearch from '../components/FieldSearch.vue';
import ResultSearch from '../components/ResultSearch.vue';

export default {
  name: 'App',
  components: {
    FieldSearch,
    ResultSearch,
  },
  data() {
    return {
      query: '',
      count: 0,
      select: '',
    };
  },
  methods: {
    apiSearch(query) {
      this.query = query.query;
      this.select = query.select;
    },
    countSearch(valor) {
      setTimeout(() => {
        this.$refs.resultSearch.queryGitHub(this.$refs.resultSearch.query);
      }, 200);

      this.count = valor;
    },
  },
};
</script>

<style>
body {
  padding: 0;
  margin: 0;
  overflow: hidden;
}

footer {
  background: #2f2f2f;
  padding: 15px;
  color: #fff;
  display: flex;
  justify-content: space-between;
  font-size: 14px;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  display: flex;
  margin-top: 0;
  align-items: initial;
  justify-content: space-between;
  flex-direction: column;
  width: 100%;
  height: 100vh;
}

.logo {
  margin: 30px auto;
  display: block;
  max-width: 100%;
  padding: 20px;
  box-sizing: border-box;
}
</style>
