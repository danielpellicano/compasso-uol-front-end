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
ul li {
  display: inline-block;
  padding: 10px 30px;
  border: 1px solid #fff;
}

ul li:first-child {
  margin-right: 15px;
}
</style>
