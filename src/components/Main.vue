<template>
  <div>

    <h4>Risultato film:</h4>
    <Card v-for="film in filmList" :key="film.id"
      :title="film.title"
      :originalTitle="film.original_title"
      :language="film.original_language"
      :vote="film.vote_average"
      :imgPath="film.poster_path"/>

    <h4>Risultato serie tv:</h4>
    <Card v-for="serie in serieList" :key="serie.id"
      :title="serie.name"
      :originalTitle="serie.original_name"
      :language="serie.original_language"
      :vote="serie.vote_average"
      :imgPath="serie.poster_path"/>

  </div>
</template>

<script>

import Card from '../components/Card.vue'

export default {
    name: "Main",

    props: {
        filmList: Array,
        serieList: Array
    },

    components: {
    Card
  },
}

</script>

<style>

</style>