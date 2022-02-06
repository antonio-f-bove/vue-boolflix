<template>
  <div class="card text-white bg-dark">
    <div class="poster">
      <img :src="getPoster(show)" class="img-fluid" />
    </div>
    <div class="info card-body">
      <div><span>Titolo: </span>{{ show.name }}</div>
      <div><span>Titolo originale: </span>{{ show.original_name }}</div>
      <div>
        <span>Voto: </span><span>{{ show.vote_average }}</span>
      </div>
      <div>
        <span>Lingua: </span>{{ show.original_language }}
        <span class="flag">
          <img class="img-fluid" :src="getFlag(show.origin_country)" />
        </span>
      </div>
    </div>
  </div>
</template>

<script>
// import axios from 'axios';
export default {
  props: {
    show: Object,
  },
  data () {
    return {
      productionCountries: [],
    }
  },
  methods: {
    getFlag (country) {
      return `http://www.geognos.com/api/en/countries/flag/${country}.json`
    },
    getPoster (show) {
      if (show.poster_path !== null) {
        return `https://image.tmdb.org/t/p/w342/${show.poster_path}`
      } else {
        // TODO! non funziona
        return '../assets/no-poster.png'
      }
    }
  }
}
</script>

<style lang="scss" scoped>
@import '../style/card-style.scss';

</style>
