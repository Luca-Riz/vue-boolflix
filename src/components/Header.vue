<template>
  <div class="header d-flex justify-content-between align-items-center">
    <div class="title m-3">
      <h1 class="text-uppercase fw-bolder">{{ msg }}</h1>
    </div>

    <div class="search m-3 d-flex">

      <input class="form-control me-2"
      type="text"
      placeholder="Digita cosa cercare"
      v-model.trim="inputText">

      <button class="btn btn-dark"
      type="submit"
      @click="setApi">
      Search
      </button>

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

h1{
  font-size: 4rem;
  color:red;
}

</style>
