<template>
  <div :class="$style.contador">
    <h2>Clicked {{ count }} times.</h2>
    <button @click="increment">increment</button>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        count: 0
      }
    },
    methods: {
      increment() {
        this.count++
      }
    }
  }
</script>

<style module>
  .contador {
    background: black;
    color: white;
    text-align: center;
  }

</style>