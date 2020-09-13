<template>
  <div class="page-results">
    <!--<form v-on:submit.prevent="queryGitHub(query)">
      <input type="text" placeholder="User Github..." v-model="query" />
      <input type="submit" value="Search" />
    </form>-->
    <div class="results" v-if="results">
      <div class="img-block">
        <img v-if="results.avatar_url" v-bind:src="results.avatar_url" />
      </div>
      <div class="info-block">
        <h2>{{ results.name }}</h2>
        <div>{{ results.bio }}</div>
        <div>{{ results.location }}</div>
        <div v-if="results.followers">Followers: {{ results.followers }}</div>
        <div v-if="results.following">Following: {{ results.following }}</div>
        <a v-if="results.blog" v-bind:href="results.blog">Go to website</a>
        {{ results.message }}
        <buttons-repo />
      </div>
    </div>
  </div>
</template>

<script>
import ButtonsRepo from "./ButtonsRepo.vue";

export default {
  name: "ResultSearch",
  components: { ButtonsRepo },
  props: ["query", "countSearch"],
  data() {
    return {
      msg: "GitHub Search",
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
  watch: {
    countSearch() {
      this.queryGitHub(this.query);
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
  margin: 0px auto;
  width: 80%;
  max-width: 600px;
  display: flex;
  padding: 15px;
}
.results img {
  width: 150px;
  border-radius: 100%;
  border: 4px solid #000;
  box-shadow: -8px 8px 20px 6px #c27e2a61;
}

.results .info-block {
  text-align: left;
  padding-left: 20px;
}

.page-results {
  background: #272223;
  color: #eee;
}

ul {
  list-style-type: none;
  padding: 0;
  display: flex;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
