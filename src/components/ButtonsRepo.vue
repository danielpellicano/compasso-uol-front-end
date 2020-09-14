<template>
  <div>
    <ul class="btns">
      <li>
        <button
          :class="showRepoUser ? 'active' : ''"
          @click="
            userRepoGet();
            showRepoUser = true;
          "
        >
          <i class="fa fa-user-plus"></i>User Repos
        </button>
      </li>
      <li>
        <button
          :class="showRepoStarred ? 'active' : ''"
          @click="
            userStarredGet();
            showRepoStarred = true;
          "
        >
          <i class="fa fa-star"></i>Starred Repos
        </button>
      </li>
    </ul>

    <div
      class="userRepo animate__animated animate__bounceIn"
      v-if="showRepoUser"
    >
      <h3>User Repo</h3>
      <ul class="listRepo">
        <li v-for="item in userRepoData" :key="item.name">
          <a :href="item.html_url">{{ item.name }}</a>
        </li>
      </ul>
    </div>

    <div
      class="starredRepo animate__animated animate__bounceIn"
      v-if="showRepoStarred"
    >
      <h3>Starred Repo</h3>
      <ul class="listRepo">
        <li v-for="item in userStarredData" :key="item.name">
          <a :href="item.html_url">{{ item.name }}</a>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ButtonsRepo',
  data() {
    return {
      showRepoUser: false,
      showRepoStarred: false,
      userRepoUrl: '',
      starredRepoUrl: '',
      userRepoData: [],
      userStarredData: [],
      count: 0,
    };
  },
  created: function() {
    /*this.userRepoGet();*/
  },
  methods: {
    userRepoGet() {
      this.showRepoStarred = false;
      this.userRepoUrl = this.$attrs.userRepo;
      fetch(this.userRepoUrl)
        .then(j => {
          return j.json();
        })
        .then(r => {
          this.$emit('userRepoData', r);
          this.userRepoData = r;
        });
    },
    userStarredGet() {
      this.showRepoUser = false;

      this.starredRepoUrl = this.$attrs.starredRepo;
      fetch(this.starredRepoUrl)
        .then(j => {
          return j.json();
        })
        .then(r => {
          this.$emit('userStarredData', r);
          this.userStarredData = r;
        });
    },
  },
};
</script>

<style scoped>
ul {
  list-style-type: none;
  padding: 0;
  display: flex;
  justify-content: space-between;
}
ul li {
  display: inline-block;
  border: 1px solid #fff;
  transition: all 0.3s ease-out;
}
ul li:hover {
  background: #f8bb23;
  color: #231f20;
}

ul li:first-child {
  margin-right: 15px;
}

ul li button {
  background: none;
  padding: 10px 30px;
  border: 0;
  color: #fff;
  font-size: 14px;
  cursor: pointer;
}

ul li i {
  margin-right: 7px;
}

.listRepo {
  display: block;
}

.listRepo li {
  border: 0;
  width: 100%;
}

.listRepo li a {
  color: #fff;
  text-decoration: none;
  background: url('../assets/img/list-arrow.png') no-repeat 5px;
  background-size: 10px;
  padding-left: 20px;
  padding: 7px 20px;
  display: block;
}

.listRepo li a:hover {
  color: #231f20;
}
</style>
