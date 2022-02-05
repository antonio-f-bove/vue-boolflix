<template>
  <div class="card text-white bg-dark">
    <div class="poster d-none">
      <img src="" alt="" />
    </div>
    <div class="info card-body">
      <div><span>Titolo: </span>{{ movie.title }}</div>
      <div><span>Titolo originale: </span>{{ movie.original_title }}</div>
      <div>
        <span>Voto: </span><span>{{ movie.vote_average }}</span>
      </div>
      <div>
        <span>Lingua: </span>{{ movie.original_language }}
        <span class="flag">
          <img class="img-fluid" :src="getFlag(movie)" />
        </span>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
export default {
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
        axios
          .get(`https://api.themoviedb.org/3/movie/${movie.id}?api_key=1907f9ddd62b6188f8c04f21ba63f5ab`)
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
    }
  }
}
</script>

<style lang="scss" scoped>
.info {
  span {
    font-weight: bold;
  }

  span.flag {
    display: inline-block;
    height: 1rem;
    width: 1.33333333rem;
  }
}
</style>
