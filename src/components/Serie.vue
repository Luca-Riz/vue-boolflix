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
    urlFlagCreate(){
      this.urlFlag = require("../assets/flag/" + this.language + ".png");
      this.urlImg = "https://image.tmdb.org/t/p/" + "w342" + this.imgPath;
      // console.log(this.urlImg);
      this.starVote = Math.round(this.vote / 2);
      // console.log(this.starVote);
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
