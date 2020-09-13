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
img {
  margin-bottom: 30px;
}
form {
  background: #eee;
  padding: 10px;
}
</style>
