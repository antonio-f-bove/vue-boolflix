<template>
  <div id="app">
    <the-header @search="searchDatabase"/>
    <the-main :movies="searchResults"/>
  </div>
</template>

<script>
import axios from 'axios'
import TheHeader from './components/TheHeader.vue';
import TheMain from './components/TheMain.vue'

export default {
  name: "App",
  components: {
    TheHeader,
    TheMain
  },
  data() {
    return {
      searchResults:[],

    }
  },
  methods: {
    searchDatabase (query) {
      //API call
      const apiTemplate = `https://api.themoviedb.org/3/search/movie?query=${query}&language=it&api_key=1907f9ddd62b6188f8c04f21ba63f5ab`;

      axios
        .get(apiTemplate)
        .then((result) => {
          this.searchResults = result.data.results;
          console.log()
        });
    }
  }
};
</script>

<style lang="scss">
@import '~bootstrap/scss/bootstrap.scss';

#app {
  background-color: #111;
  height: 100vh;
}
</style>
