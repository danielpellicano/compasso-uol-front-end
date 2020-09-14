<template>
  <div id="app" class="home">
    <img
      class="logo"
      alt="Uol Compasso"
      src="./assets/img/uol-compasso.svg"
      width="500"
    />
    <FieldSearch @search="apiSearch" @countSearch="countSearch" />
    <ResultSearch ref="resultSearch" :query="query"  />
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'Home',
  components: {
    HelloWorld
  }
}
</script>

<style >
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
