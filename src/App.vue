<template>
  <div id="app">
    
    <Header msg="Boolflix" @apiMod="newApi" /> 

    <h4>Risultato film:</h4>
    <Film v-for="film in filmList" :key="film.id"
      :title="film.title"
      :originalTitle="film.original_title"
      :language="film.original_language"
      :vote="film.vote_average"
      :imgPath="film.backdrop_path"/>

    <h4>Risultato serie tv:</h4>
    <Serie v-for="serie in serieList" :key="serie.id"
      :title="serie.name"
      :originalTitle="serie.original_name"
      :language="serie.original_language"
      :vote="serie.vote_average"
      :imgPath="serie.backdrop_path"/>
    
  </div>
</template>

<script>
import axios from 'axios';
import Header from './components/Header.vue'
import Film from './components/Film.vue'
import Serie from './components/Serie.vue'

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
    Film,
    Serie
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
