<template>
  <div class="header">
    <div class="title">
      <h1>{{ msg }}</h1>
    </div>

    <div class="search">
      <input 
      type="text"
      placeholder="Digita cosa cercare"
      v-model.trim="inputText">

      <button
      type="submit"
      @click="setApi">Search</button>

    </div>

  </div>
</template>

<script>
export default {
  name: 'Header',
  props: {
    msg: String
  },

  data() {
    return {
        inputText:'',
        api: '',
    }
  },

  methods: {
    setApi: function(){
      console.log(this.inputText);
      //! da cancellare dopo aver ricostruito in App l'url
      // this.api = "https://api.themoviedb.org/3/search/movie?api_key=e14a682f2cb51ebef668a83973649087&query="
      // + this.inputText + 
      // "&language=it-IT";
      // console.log(this.api);
      this.$emit( 'apiMod', this.inputText);
    }
  },
}
</script>

<style scoped lang="scss">

</style>
