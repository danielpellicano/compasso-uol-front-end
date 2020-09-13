<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <form v-on:submit.prevent="queryGitHub(query)">
      <input type="text" placeholder="User Github..." v-model="query" />
      <input type="submit" value="Search" />
    </form>
    <div class="results" v-if="results">
      <img v-if="results.avatar_url" v-bind:src="results.avatar_url" />
      <h2>{{ results.name }}</h2>
      <div>{{ results.bio }}</div>
      <div>{{ results.location }}</div>
      <div v-if="results.followers">Followers: {{ results.followers }}</div>
      <div v-if="results.following">Following: {{ results.following }}</div>
      <a v-if="results.blog" v-bind:href="results.blog">Go to website</a>
      {{ results.message }}
    </div>
    <buttons-repo />
  </div>
</template>

<script>
import ButtonsRepo from "./ButtonsRepo";

export default {
  name: "ResultSearch",
  components: "ButtonsRepo",
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

<style scoped>
h1,
h2 {
  font-weight: normal;
}
.results {
  margin: 20px auto;
  width: 80%;
  max-width: 600px;
}
.results img {
  float: left;
  width: 250px;
  border-radius: 100%;
  border: 4px solid #000;
  box-shadow: -8px 8px 20px 6px #c27e2a61;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
