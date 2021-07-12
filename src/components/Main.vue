<template>
  <div class="hello">
    <h2>{{ msg }}</h2>


    <ul v-for="(film,index) in filmList" :key="index">
      <li >{{ film.title }}</li>
    </ul>

    
  </div>
</template>

<script>
import axios from 'axios';
export default {
  name: 'Main',
  props: {
    msg: String

  },

 

  data() {
      return {
          apiURL : 'https://api.themoviedb.org/3/search/movie?api_key=e14a682f2cb51ebef668a83973649087&query=avatar&language=it-IT',
          filmList : [],
          loading: true,
          searchText: ''
      }
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
  }
  
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

</style>
