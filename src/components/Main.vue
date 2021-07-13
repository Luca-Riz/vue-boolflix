<template>
  <div class="hello">
    <h2>{{ msg }}</h2>

    <ul>
      <li><strong> Titolo: </strong> {{ title }}</li> 
      <li>Titolo originale: {{ originalTitle }}</li>
      <li>
        Lingua originale:  
        <img :src="urlFlagCreate()" :alt="language">
      </li>
      <li>Voto medio: {{ vote }}</li>
    </ul>
    
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
  },

  data() {
    return {
      urlFlag:'',
    }
  },

  methods: {
    urlFlagCreate(){
      this.urlFlag = require("../assets/flag/" + this.language + ".png");
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
