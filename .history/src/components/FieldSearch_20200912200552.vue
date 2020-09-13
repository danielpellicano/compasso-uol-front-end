<template>
  <form v-on:submit.prevent="queryGitHub(query)">
    <input type="text" placeholder="User Github..." v-model="query" />
    <input type="submit" value="Search" />
  </form>
</template>

<script>
export default {
  name: "FieldSearch",
  data() {
    return {
      query: "",
      countSearch: 0,
    };
  },
  watch: {
    query() {
      this.$emit("search", this.query);
    },
  },
  methods: {
    queryGitHub() {
      this.$emit("countSearch", this.countSearch + 2);
    },
  },
};
</script>

<style scoped>
form {
  background: #eee;
  padding: 10px;
}

form input[type="text"] {
  padding: 10px;
  width: 15%;
}

form input[type="submit"] {
  background: #231f20 url(@/assets/search.png) no-repeat;
  color: #fff;
  padding: 10px 30px;
  border: 2px solid #231f20;
  border-radius: 0 10px 10px 0;
}
</style>
