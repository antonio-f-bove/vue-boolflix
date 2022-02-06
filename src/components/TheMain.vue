<template>
  <main>
    <div v-if="movies.length" class="container">
      <h2>MOVIES</h2>
      <div class="row strip">
        <movie-card v-for="movie in movies" :key="movie.id" :movie="movie" class="col-2" />
      </div>
    </div>
    <div v-if="shows.length" class="container">
      <h2>TV</h2>
      <div class="row strip">
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
    TvShowCard
  },
  props: {
    movies: Array,
    shows: Array,
  }
}
</script>

<style lang="scss" scoped>

.row.strip {
  height: 282px;
  flex-wrap: nowrap;
  align-items: center;
  overflow-x: scroll;
  overflow-y: hidden;
}
</style>