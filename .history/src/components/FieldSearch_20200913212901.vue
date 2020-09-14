<template>
  <form v-on:submit.prevent="queryGitHub">
    <input type="text" placeholder="User Github..." v-model="query" />
    {{ selected }}
    <select v-model="selected">
      <option disabled value="">Escolha um item</option>
      <option value="repo">Reposit</option>
      <option value="user">User</option>
    </select>
    <input type="submit" @click="queryGitHub" value="Search User" />
  </form>
</template>

<script>
export default {
  name: "FieldSearch",
  data() {
    return {
      query: "",
      countSearch: 0,
      selected: "",
    };
  },
  mounted() {
    this.query = "";
  },
  watch: {
    query: {
      handler: function() {
        this.$emit("search", {
          query: this.query,
          select: this.selected,
        });
      },
      deep: true,
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
  background: #231f20 url("../assets/img/search.svg") no-repeat 109px;
  background-size: 15px;
  color: #fff;
  padding: 10px 50px 10px 30px;
  border: 2px solid #231f20;
  border-radius: 0 10px 10px 0;
  cursor: pointer;
  transition: all 0.3s ease-out;
}

form input[type="submit"]:hover {
  border-color: #f8bb23;
  color: #231f20;
  background-color: #f8bb23;
}
</style>
