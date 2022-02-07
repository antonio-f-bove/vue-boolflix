<template>
  <main>
    <div v-if="movies.length" class="container">
      <h4>MOVIES</h4>
      <div class="row strip mb-3">
        <movie-card v-for="movie in movies" :key="movie.id" :movie="movie" class="col-2" />
      </div>
    </div>
    <div v-if="shows.length" class="container">
      <h4>TV</h4>
      <div class="row strip mb-3">
        <tv-show-card v-for="show in shows" :key="show.id" :show="show" class="col-2" />
      </div>
    </div>

  </main>
</template>

<script>
import MovieCard from './MovieCard.vue'
import TvShowCard from './TvShowCard.vue'

export default {
  components: {
    MovieCard,
    TvShowCard,
  },
  props: {
    movies: Array,
    shows: Array,
  },
  computed: {
    // moviesRange() {
    // }
  }
}
</script>

<style lang="scss" scoped>
@import '../style/variables.scss';

main {
  margin-top: 90px;
}

.row.strip {
  height: 282px;
  flex-wrap: nowrap;
  align-items: center;
  overflow-x: scroll;
  overflow-y: hidden;
  border-radius: none;
}

h4 {
  color: $boolflix-red;
  font-weight: bolder;
}
</style>