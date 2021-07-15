<template>
  <div class="main m-3">

    <div @click="caricaCast" class="card" >
      
      <!-- inizio dati film -->
      <div class="data card-body">
        <ul>
          <li class="card-title fs-3"><strong> Titolo: </strong> {{ title }}</li> 
          <li v-if="this.title !== this.originalTitle" class="card-subtitle mb-2"> Titolo originale: {{ originalTitle }}</li>
          <li class="d-flex align-items-center card-text ">
            <strong>Lingua originale:</strong>    
              <div v-if="flags.includes( language )" class="flag">
                <img :src="urlFlagCreate()" :alt="language" class="ms-2">
              </div>
              <div v-else> {{ language }} </div>
          </li>
          <li v-if="this.starVote != 0">
            <!-- ul stelline voto -->
            <ul class="d-flex card-text">
              <strong>Voto medio: </strong> 
              <li v-for="(item, i) in starVote" :key="i">
                <i class="fas fa-star"></i>
              </li>
              <li v-for="(item, i) in starVoteNeg" :key="'A'+ i">
                <i class="far fa-star"></i>
              </li>
            </ul>
            <!-- fine ul stelline voto -->
          </li>
          <li v-if="overview" class="overwiew"> 
            <strong>Panoramica: </strong> {{ overview }}
            
          </li>
          <li>
            <ul v-if="filmCast"> Cast:
              <li v-for="(item, i) in filmCast" :key="'B'+ i" class="ms-5"> {{ item.name }} </li>
            </ul>
          </li>

        </ul> 
      </div>
      <!-- fine dati film -->

      <!-- inizio copertina -->
      <div class="cover">
        <img :src="urlImg" :alt="title">
      </div>
      <!-- fine copertina -->

    </div>

  </div>

</template>

<script>
import axios from 'axios';
export default {
  name: 'Main',
  urlFlag: '',
  urlImg: '',
  props: {
    id: Number,
    msg: String,
    title: String,
    originalTitle: String,
    language: String,
    vote: Number,
    overview: String,
    imgPath: String,
    actorsName: String,
  },

  data() {
    return {
      flags: [ "en", "es", "hr", "it", "pt"],
      urlImg: '',
      starVote: 0,
      starVoteNeg: 0,
      filmCast:"",
    }
  },

  methods: {

    caricaCast(){
      if( this.filmCast == '' ){
        axios.get('https://api.themoviedb.org/3/movie/' + this.id + '/credits?api_key=e14a682f2cb51ebef668a83973649087&language=it-IT')
        .then(  (responseCast) => { this.filmCast = responseCast.data.cast; console.log(this.filmCast); })
      }
    },

    urlFlagCreate(){
      this.urlFlag = require("../assets/flag/" + this.language + ".png");

      // calcolo numero stelle piene, se 0 o vuoto, setta a 0
      if (parseInt(this.vote) != 0){
        this.starVote = Math.round(parseInt(this.vote) / 2);
      } else {this.starVote = 0}

      //img url se presente
      if (this.imgPath != null){
        this.urlImg = "https://image.tmdb.org/t/p/" + "w342" + this.imgPath;
      } else { this.urlImg = require("../assets/img/notFound.png")}

      //starVoteNeg
      this.starVoteNeg = 5 - this.starVote;

      return this.urlFlag
    }
  },



}
</script>

<style scoped lang="scss">

</style>
