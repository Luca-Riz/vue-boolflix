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
      // console.log(this.inputText);
      this.$emit( 'apiMod', this.inputText);
    }
  },
}
</script>

<style scoped lang="scss">

  
</style>
