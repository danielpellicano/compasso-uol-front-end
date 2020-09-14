<template>
  <form v-on:submit.prevent="queryGitHub" id="form">
    <select v-model="selected">
      <option disabled value="">Escolha um item</option>
      <option value="repo">Reposit</option>
      <option value="user">User</option>
    </select>
    <input type="text" placeholder="User Github..." v-model="query" />
    <input type="submit" value="Search User" />
  </form>
</template>

<script>
export default {
  name: 'FieldSearch',
  data() {
    return {
      query: '',
      countSearch: 0,
      selected: '',
    };
  },
  mounted() {
    this.query = '';
  },
  watch: {
    query: {
      handler: function() {
        this.$emit('search', {
          query: this.query,
          select: this.selected,
        });
      },
      deep: true,
    },
    selected() {
      this.$emit('search', {
        query: this.query,
        select: this.selected,
      });
    },
  },
  methods: {
    queryGitHub() {
      if (this.selected) {
        this.$emit('countSearch', this.countSearch + 2);
      } else {
        alert('Selecione o que vocÊ quer pesquisar');
      }
    },
  },
};
</script>

<style scoped>
form {
  background: #eee;
  padding: 10px;
}

form input[type='text'] {
  padding: 10px;
  width: 15%;
  outline: none;
}

form input[type='submit'] {
  background: #231f20 url('../assets/img/search.svg') no-repeat 109px;
  background-size: 15px;
  color: #fff;
  padding: 10px 50px 10px 30px;
  border: 2px solid #231f20;
  border-radius: 0 10px 10px 0;
  cursor: pointer;
  transition: all 0.3s ease-out;
}

form input[type='submit']:hover {
  border-color: #f8bb23;
  color: #231f20;
  background-color: #f8bb23;
}

form select {
  padding: 10px;
  margin-right: -1px;
}

@media only screen and (max-width: 600px) {
  form {
    padding: 12px;
    width: 100%;
    box-sizing: border-box;
  }

  form select {
    padding: 10px;
    margin-right: 0;
    width: 100%;
    box-sizing: border-box;
    margin-bottom: 10px;
  }

  form input[type='text'] {
    padding: 10px;
    width: 100% !important;
    outline: none;
    box-sizing: border-box;
    margin-bottom: 10px;
  }
  form input[type='submit'][data-v-32159c42] {
    background: #231f20 url(/img/search.00ec8028.svg) no-repeat 94%;
    background-size: 15px;
    color: #fff;
    padding: 10px 50px 10px 30px;
    border-radius: 0;
    width: 100%;
  }
}
</style>
