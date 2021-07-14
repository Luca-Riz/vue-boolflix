<template>
  <div class="main m-3">

    <div class="card">
      
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
          <li>
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
          <li class="overwiew"> 
            <strong>Panoramica: </strong> {{ overview }}
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

export default {
  name: 'Main',
  urlFlag: '',
  urlImg: '',
  props: {
    msg: String,
    title: String,
    originalTitle: String,
    language: String,
    vote: Number,
    overview: String,
    imgPath: String,
  },

  data() {
    return {
      flags: [ "en", "es", "hr", "it", "pt"],
      urlImg: '',
      starVote: 0,
      starVoteNeg: 0
    }
  },

  methods: {
    // flag url
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
