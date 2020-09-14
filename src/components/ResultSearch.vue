<template>
  <div
    class="page-results animate__animated animate__backInLeft"
    v-if="results"
  >
    <!--<form v-on:submit.prevent="queryGitHub(query)">
      <input type="text" placeholder="User Github..." v-model="query" />
      <input type="submit" value="Search" />
    </form>-->
    <div
      class="results"
      v-if="
        (!lodash.has(results, 'message') && select == 'user') || select == ''
      "
    >
      <div class="img-block">
        <img
          v-if="lodash.has(results, 'avatar_url')"
          v-bind:src="results.avatar_url"
        />
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
        <buttons-repo :userRepo="userRepo" :starredRepo="starredRepo" />
      </div>
    </div>
    <div v-else-if="select == 'repo'">
      <ul class="list-starred">
        <li v-for="item in results['items']" :key="item.name">
          <a :href="item.url" target="_blank">{{ item.name }}</a>
        </li>
      </ul>
    </div>
    <div class="not-found" v-else>
      <h3>Usuário não encontrado</h3>
      <p>Por favor faça uma nova busca</p>
    </div>
  </div>
</template>

<script>
import ButtonsRepo from './ButtonsRepo.vue';
import lodash from 'lodash';
export default {
  name: 'ResultSearch',
  components: { ButtonsRepo },
  props: ['query', 'countSearch', 'select'],
  data() {
    return {
      results: null,
      userRepo: null,
      starredRepo: null,
      lodash: lodash,
    };
  },
  mounted() {
    if (typeof this.$route.params.slug !== 'undefined') {
      this.queryGitHub(this.$route.params.slug);
    }
  },
  methods: {
    queryGitHub(q) {
      let self = this;
      if (this.select == '' || this.select == 'user') {
        fetch('https://api.github.com/users/' + q)
          .then(j => {
            return j.json();
          })
          .then(r => {
            self.results = r;
            this.userRepo = this.results.repos_url;
            let starred_url = this.results.starred_url;
            starred_url = starred_url.split('{/owner}{/repo}')[0];
            this.starredRepo = starred_url;
          });
      } else {
        fetch('https://api.github.com/search/repositories?q=' + q)
          .then(j => {
            return j.json();
          })
          .then(r => {
            self.results = r;
            console.log(r);
          });
      }
    },
  },
  watch: {},
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
  align-items: baseline;
}
a {
  color: #fff;
}

.not-found {
  padding: 30px 10px;
}

.list-starred {
  list-style: none;
  max-width: 500px;
  margin: 0 auto;
  text-align: left;
  padding: 20px;
}

.list-starred li {
  background: url('../assets/img/list-arrow.png') no-repeat 5px;
  background-size: 10px;
  padding-left: 20px;
  margin-bottom: 7px;
}

.list-starred li a {
  text-decoration: none;
}

.list-starred li a:hover {
  color: #f7b718;
}

@media only screen and (max-width: 600px) {
  .results {
    width: 100%;
    max-width: 600px;
    display: block;
    text-align: center;
    box-sizing: border-box;
  }

  .img-block {
    justify-content: center;
  }

  .results .info-block {
    padding-left: 0;
  }
}
</style>
