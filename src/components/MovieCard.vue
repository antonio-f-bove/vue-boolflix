<template>
  <div class="card text-white bg-dark">
    <div class="poster">
      <img :src="getPoster(movie)" class="img-fluid" />
    </div>
    <div class="info card-body">
      <div><span>Titolo: </span>{{ movie.title }}</div>
      <div><span>Titolo originale: </span>{{ movie.original_title }}</div>
      <div>
        <span>Voto: </span><stars-rating :rate="movie.vote_average" />
      </div>
      <div>
        <span>Lingua: </span>
        <span class="flag">
          <img class="img-fluid" :src="getFlag(movie)" />
        </span>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import StarsRating from './StarsRating.vue'

export default {
  components: {
    StarsRating,
  },
  props: {
    movie: Object,
  },
  data () {
    return {
      productionCountries: [],
    }
  },
  methods: {
    getFlag (movie) {
      let langIso = movie.original_language;
      /* 'en' non essendo un codice iso valido, 
      con questa funzione controllo i paesi di 
      produzione e differenzio tra US e GB. 
      Non è una soluzione definitiva, e sarebbe 
      necessaria una disambiguazione 
      per tante altre lingue
      */
      if (langIso === 'en') {
        // uso movie.id per chieder piu info all'API -> paesi di produzione
        const movieApiTemplate = `https://api.themoviedb.org/3/movie/${movie.id}?api_key=1907f9ddd62b6188f8c04f21ba63f5ab`;
        
        axios
          .get(movieApiTemplate)
          .then((result) => {
            this.productionCountries = result.data.production_countries
          });

          let isUk = false;
          this.productionCountries.forEach((country) => {
            if(country.iso_3166_1 === 'GB') {
              // qui mi accontento della presenza di GB tra i paesi di produzione per dargli la bandiera
              isUk = true;
            }
          });
          if (isUk) {
            langIso = 'GB';
          } else {
            // qui entrano US e tutti gli altri anglofoni
            langIso = 'US';
          }
      }

      return `http://www.geognos.com/api/en/countries/flag/${langIso.toUpperCase()}.json`
    },
    getPoster (movie) {
      return `https://image.tmdb.org/t/p/w342/${movie.poster_path}`
    }
  }
}
</script>

<style lang="scss" scoped>
@import '../style/card-style.scss';

</style>
