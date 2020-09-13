<template>
  <ul class="btns">
    <li>
      <button :userRepo="(userRepo = '1mar')">
        <i class="fa fa-user-plus"></i>User Repos
      </button>
    </li>
    <li>
      <button :click="userStarredGet">
        <i class="fa fa-star"></i>Starred Repos
      </button>
    </li>
  </ul>
</template>

<script>
export default {
  name: "ButtonsRepo",
  data() {
    return {
      userRepo: "123",
      userStarred: "",
    };
  },
  mounted: function() {},
  methods: {
    userRepoGet() {
      alert("user repo");
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
