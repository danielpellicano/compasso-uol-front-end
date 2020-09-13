<template>
  <ul class="btns">
    <li><font-awesome-icon icon="user-secret" /> User Repos</li>
    <li>Starred Repos</li>
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
  padding: 10px;
  border: 1px solid #fff;
}

ul li:first-child {
  margin-right: 15px;
}
</style>
