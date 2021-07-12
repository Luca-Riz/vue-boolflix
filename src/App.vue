<template>
  <div id="app">
    
    <Header msg="Boolflix"/>
    <Main msg="This is the main"/>

  </div>
</template>

<script>
import Header from './components/Header.vue'
import Main from './components/Main.vue'

export default {
  name: 'App',
  components: {
    Header,
    Main
  }
}
</script>

<style lang="scss">
@import '@/style/general.scss';


</style>
