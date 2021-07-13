<template>
  <div class="main">

    <div class="card">
      <ul>
        <li><strong> Titolo: </strong> {{ title }}</li> 
        <li>Titolo originale: {{ originalTitle }}</li>
        <li class="d-flex">
          Lingua originale:   
            <div v-if="flags.includes( language )">
              <img :src="urlFlagCreate()" :alt="language">
            </div>
            <div v-else> {{ language }} </div>
        </li>
        <li>Voto medio: {{ vote }}</li>
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

  },

  data() {
    return {
      flags: [ "en", "es", "hr", "it", "pt"]
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
