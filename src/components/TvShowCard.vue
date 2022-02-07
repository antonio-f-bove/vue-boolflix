<template>
  <div class="card text-white bg-dark">
    <div class="poster">
      <img :src="getPoster(show)" class="img-fluid" />
    </div>
    <div class="info card-body">
      <div><span>Titolo: </span>{{ show.name }}</div>
      <div v-if="show.original_name !== show.name">
        <span>Titolo originale: </span>{{ show.original_name }}
      </div>
      <div>
        <span>Voto: </span><stars-rating :rate="show.vote_average" />
      </div>
      <div>
        <span>Lingua: </span>
        <span class="flag">
          <img class="img-fluid" :src="getFlag(show.origin_country)" />
        </span>
        <div class="overview" v-if="show.overview"><span>Overview: </span>{{ limitTextLength(show.overview, 150) }}</div>
      </div>
    </div>
  </div>
</template>

<script>
import StarsRating from './StarsRating.vue'

export default {
  components: {
    StarsRating,
  },
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
    },
    limitTextLength (string, length) {
      if (string.length > length) {
        return string.substring(0, length) + '...'
      } else {
        return string
      }
    }
  }
}
</script>

<style lang="scss" scoped>
@import '../style/card-style.scss';

</style>
