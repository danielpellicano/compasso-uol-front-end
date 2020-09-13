<template>
   <form v-on:submit.prevent="queryGitHub(query)">
      <input type="text" placeholder="User Github..." v-model="query" />
      <input type="submit" value="Search" />
    </form>
</template>

<script>
export default {
  name: "FieldSearch"
}
</script>

<style>

</style>