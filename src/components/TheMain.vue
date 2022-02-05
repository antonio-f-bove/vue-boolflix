<template>
  <main>
    <div class="container">
      <div class="row">
        <movie-card v-for="movie in movies" :key="movie.id" :movie="movie" class="col-2" />
      </div>
    </div>

  </main>
</template>

<script>
import MovieCard from './MovieCard.vue'

export default {
  components: {
    MovieCard,
  },
  props: {
    movies: Array,
  }
}
</script>

<style lang="scss" scoped>

</style>