<template>
  <div>
    <AppHeader/>
    <app-count/>
  </div>
</template>

<script>
  import AppCount from "./components/AppCount.vue";
  import AppHeader from './components/AppHeader.vue';

  export default {
    components: {
      AppCount,
      AppHeader
    }
  }
</script>