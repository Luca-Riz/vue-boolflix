<template>
  <div id="app">
    
    <Header msg="Boolflix"  /> 
    <!-- @inputText="apiMod" andrà dentro qui sopra -->
    <Main v-for="(film,index) in filmList" :key="index"
      :title="film.title"
      :originalTitle="film.original_title"
      :language="film.original_language"
      :vote="film.vote_average"/>   
    

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
      apiURL: 'https://api.themoviedb.org/3/search/movie?api_key=e14a682f2cb51ebef668a83973649087&query=avatar&language=it-IT',
      filmList: []
    }
  },

  components: {
    Header,
    Main
  },

  created(){
    this.getFilm();
  },




    methods: {
      getFilm(){
        axios
          .get(this.apiURL)
          .then(response => {
            // console.log(response.data);
            this.filmList = response.data.results;
            console.log(this.filmList);
          })
      }
    },

}
</script>

<style lang="scss">
@import '@/style/general.scss';


</style>
