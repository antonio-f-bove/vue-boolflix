<template>
  <div id="app">
    <the-header @search="searchDatabase" class="fixed-top" />
    <the-main :movies="movieResults" :shows="tvResults"/>
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
      results: [],
    }
  },
  computed: {
    tvResults () {
      let tvResults = this.results.filter((element) => {
        return element.media_type === 'tv'
      });
      return tvResults
    },
    movieResults () {
      let movieResults = this.results.filter((element) => {
        return element.media_type === 'movie'
      });
      return movieResults
    }
  },
  methods: {
    searchDatabase (query) {
      // multi-request API call
      const apiTemplate = `https://api.themoviedb.org/3/search/multi?query=${query}&language=it&api_key=1907f9ddd62b6188f8c04f21ba63f5ab`;

      axios
        .get(apiTemplate)
        .then((result) => {
          this.results = result.data.results;
        });
    },
  }
};
</script>

<style lang="scss">
@import '~bootstrap/scss/bootstrap.scss';

body {
  background-color: #111;
}
</style>
