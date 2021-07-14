<template>
  <div>

    <h4>Risultato film:</h4>
    <Film v-for="film in filmList" :key="film.id"
      :title="film.title"
      :originalTitle="film.original_title"
      :language="film.original_language"
      :vote="film.vote_average"
      :imgPath="film.backdrop_path"/>

    <h4>Risultato serie tv:</h4>
    <Serie v-for="serie in serieList" :key="serie.id"
      :title="serie.name"
      :originalTitle="serie.original_name"
      :language="serie.original_language"
      :vote="serie.vote_average"
      :imgPath="serie.backdrop_path"/>

  </div>
</template>

<script>

import Film from '../components/Film.vue'
import Serie from '../components/Serie.vue'

export default {
    name: "Main",

    props: {
        filmList: Array,
        serieList: Array
    },

    components: {
    Film,
    Serie
  },
}

</script>

<style>

</style>