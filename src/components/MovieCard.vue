<template>
  <div class="card">
    <div class="poster d-none">
      <img src="" alt="">
    </div>
    <div class="info card-body">
      <div>Titolo: {{movie.title}}</div>
      <div>Titolo originale: {{movie.original_title}}</div>
      <div>Voto: <span>{{movie.vote_average}}</span></div>
      <div>Lingua: {{movie.original_language}}</div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    movie: Object,
  }
}
</script> 

<style lang="scss" scoped>

</style>