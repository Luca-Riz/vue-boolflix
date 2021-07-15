<template>
  <div id="app">

    <div class="container-fluid">

      <!-- <div class="headers"> -->
        <Header msg="Boolflix" @apiMod="newApi" /> 
      <!-- </div> -->

      <!-- <div> -->
        <Main :filmList="filmList" :serieList="serieList" :filmCast="filmCast"/> 
      <!-- </div> -->

    </div>
    
  </div>
</template>

<script>
import axios from 'axios';
import Header from './components/Header.vue'
import Main from './components/Main.vue'

export default {
  name: 'App',
 
  data(){
    return {
      apiUrl: 'https://api.themoviedb.org/3/search/movie',
      apiUrlSerie: 'https://api.themoviedb.org/3/search/tv',
      apiKey: 'e14a682f2cb51ebef668a83973649087',
      language: 'it-IT',
      languageSerie: 'it_IT',
      filmList: [],
      serieList: [],
      filmCast: []
    }
  },

  components: {
    Header,
    Main
  },

  mounted() {
    // chiamata axios per film e serie tv del momento
    axios
      .all([
        axios.get('https://api.themoviedb.org/3/movie/popular?api_key=e14a682f2cb51ebef668a83973649087&language=it-IT&page=1'),
        axios.get('https://api.themoviedb.org/3/tv/popular?api_key=e14a682f2cb51ebef668a83973649087&language=it-IT&page=1'),
      ])
      .then(axios.spread( (responseFilm, responseTv) => {
          this.filmList = responseFilm.data.results;
          this.serieList = responseTv.data.results;
      }));
  },

  methods: {
    //* creo il mio url
    newApi(apiModify){

      const request = {
        params: {
          api_key: this.apiKey,
          language: this.language,
          query: apiModify
        }
      }

      // chiamata api per search
      axios
        .all([
          axios.get(this.apiUrl, request),
          axios.get(this.apiUrlSerie, request),
        ])
        .then(axios.spread( (responseFilm, responseTv) => {
          this.filmList = responseFilm.data.results;
          this.serieList = responseTv.data.results;
        }));



      axios
        .get('https://api.themoviedb.org/3/movie/19995/credits?api_key=e14a682f2cb51ebef668a83973649087&language=it-IT')
        .then(response => (this.filmCast = response.data.cast, console.log(this.filmCast)))
        .catch(error => console.log(error));

      
    }
  },

}
</script>

<style lang="scss">

@import '@/style/general.scss';
@import '@/style/card.scss';

</style>
