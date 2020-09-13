<template>
  <div>
  <ul class="btns">
    <li>
      <button :click="userRepoGet">
        <i class="fa fa-user-plus"></i>User Repos
      </button>
    </li>
    <li>
      <button :click="userStarredGet">
        <i class="fa fa-star"></i>Starred Repos
      </button>
    </li>
  </ul>

  <ul class="listRepo">
    <li :v-for="item in userRepoData" :key="item">{{userRepoData[name]}}</li>
  </ul>

  </div>
</template>

<script>
export default {
  name: "ButtonsRepo",
  data() {
    return {
      userRepoUrl: "",
      userRepoData: [],
      userStarred: "",
    };
  },
  mounted: function() {
    this.userRepoGet();
  },
  methods: {
    userRepoGet() {
      this.userRepoUrl = this.$attrs.userRepo;
      fetch(this.userRepoUrl)
        .then((j) => {
          return j.json();
        })
        .then((r) => {
          this.userRepoData = r;
          console.log(r);
        });
    },
    userStarredGet() {
      alert("starred");
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
</style>
