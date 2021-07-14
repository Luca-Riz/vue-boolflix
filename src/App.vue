<template>
  <div id="app">
    
    <Header msg="Boolflix" @apiMod="newApi" /> 

    <Main :filmList="filmList" :serieList="serieList" /> 
    
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
      filmList: '',
      serieList: ''
    }
  },

  components: {
    Header,
    Main

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

      axios
        .all([
          axios.get(this.apiUrl, request),
          axios.get(this.apiUrlSerie, request)
        ])
        .then(axios.spread( (responseFilm, responseTv) => {
          this.filmList = responseFilm.data.results;
          this.serieList = responseTv.data.results;
        }))

    }
  },

}
</script>

<style lang="scss">
@import '@/style/general.scss';

</style>
