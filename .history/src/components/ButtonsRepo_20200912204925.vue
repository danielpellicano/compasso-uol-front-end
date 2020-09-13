<template>
  <ul class="btns">
    <li><i class="fa fa-user-plus"></i>User Repos</li>
    <li><i class="fa fa-star"></i>Starred Repos</li>
  </ul>
</template>

<script>
export default {
  name: "ButtonsRepo",
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
  padding: 10px 30px;
  border: 1px solid #fff;
  cursor: pointer;
}
ul li:hover {
  background: #f8bb23;
  color: #231f20;
}

ul li:first-child {
  margin-right: 15px;
}

ul li i {
  margin-right: 7px;
}
</style>
