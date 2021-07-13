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
      apiKey: 'e14a682f2cb51ebef668a83973649087',
      language: 'it-IT',
      apiUrlSerie: 'https://api.themoviedb.org/3/search/tv',
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
      axios
        // film
        .get(this.apiUrl, {
          params: {
            api_key: this.apiKey,
            language: this.language,
            query: apiModify
          }
        })

        //film
        .then(response => {
          // console.log(response.data);
          this.filmList = response.data.results;
          console.log(this.filmList);
        })

      axios
        //serie
        .get(this.apiUrlSerie, {
          params: {
            api_key: this.apiKey,
            language: this.languageSerie,
            query: apiModify
          }
        })       

        //serie
        .then(responseSerie => {
          // console.log(response.data);
          this.serieList = responseSerie.data.results;
          console.log(this.serieList);
        })

        .catch(error => {
          console.log("Errore : " + error);
        })
    }
  },

}
</script>

<style lang="scss">
@import '@/style/general.scss';

</style>
