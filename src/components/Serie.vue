<template>
  <div class="main">

    <div class="card">
      <ul>
        <li><strong> Titolo: </strong> {{ title }}</li> 
        <li>
          <img :src="urlImg" alt="">
        </li>
        <li>Titolo originale: {{ originalTitle }}</li>
        <li class="d-flex">
          Lingua originale:   
            <div v-if="flags.includes( language )">
              <img :src="urlFlagCreate()" :alt="language">
            </div>
            <div v-else> {{ language }} </div>
        </li>
        <li>Voto medio: {{ starVote }}</li>
      </ul>    
    </div>

  </div>

</template>

<script>

export default {
  name: 'Main',
  urlFlag: '',
  props: {
    msg: String,
    title: String,
    originalTitle: String,
    language: String,
    vote: Number,
    imgPath: String,
  },

  data() {
    return {
      flags: [ "en", "es", "hr", "it", "pt"],
      urlImg: '',
      starVote: ''
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
      if (this.imgPath !== null){
        this.urlImg = "https://image.tmdb.org/t/p/" + "w342" + this.imgPath;
      } 

      return this.urlFlag
    }
  },

}
</script>

<style scoped lang="scss">

  img {
    height: 30px;
  }

</style>
