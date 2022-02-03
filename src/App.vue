<template>
  <div id="app">
    <the-header />
    <the-main />
  </div>
</template>

<script>
// import axios from 'axios'
import TheHeader from './components/TheHeader.vue';
import TheMain from './components/TheMain.vue'

export default {
  name: "App",
  components: {
    TheHeader,
    TheMain
  },
};
</script>

<style lang="scss">
@import '~bootstrap/scss/bootstrap.scss'
</style>
