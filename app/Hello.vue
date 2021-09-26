<template>
  <div>
    <h1>{{ title }}</h1>
    <input v-model="title">
  </div>
</template>

<script>
  export default {
    name: "Hello",
    data: function() {
      return {
        title: 'Hello VueJs'
      }
    }
  }
</script>

<style scoped>

</style>