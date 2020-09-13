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
        <div class="bio">{{ results.bio }}</div>
        <div class="row">
          <div class="local">
            <i class="fa fa-map-marker"></i>{{ results.location }}
          </div>
          <a v-if="results.blog" v-bind:href="results.blog"
            ><i class="fa fa-globe"></i> Go to website</a
          >
        </div>
        {{ results.message }}
        <buttons-repo :userRepo="userRepo" />
      </div>
    </div>
  </div>
</template>

<script>
import ButtonsRepo from "./ButtonsRepo.vue";

export default {
  name: "ResultSearch",
  components: { ButtonsRepo },
  props: ["query", "countSearch", "userRepo"],
  data() {
    return {
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
          this.userRepo = this.results.repos_url;
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
h2 {
  font-weight: normal;
  margin-bottom: 5px;
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
  border: 4px solid #fff;
}

.results .info-block {
  text-align: left;
  padding-left: 20px;
}

.row {
  display: flex;
  justify-content: space-between;
}

.bio {
  margin-bottom: 20px;
}

i {
  margin-right: 7px;
}

.page-results {
  background: #272223;
  color: #eee;
}

.img-block {
  display: flex;
  align-items:initial;
}
a {
  color: #fff;
}
</style>
