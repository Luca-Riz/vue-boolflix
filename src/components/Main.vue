<template>
  <div class="">

    <h4 class="fs-2 mx-3">Film:</h4>
    <div class="film d-flex flex-wrap justify-content-between">
        <Card :filmCast="filmCast"
          v-for="film in filmList" :key="film.id"
          :title="film.title"
          :originalTitle="film.original_title"
          :language="film.original_language"
          :vote="film.vote_average"
          :imgPath="film.poster_path"
          :id="film.id"
          :overview="film.overview"/>
    </div>

    <h4 class="fs-2 mx-3">Serie tv:</h4>
    <div class="serie d-flex flex-wrap justify-content-between">
        <Card v-for="serie in serieList" :key="serie.id"
          :title="serie.name"
          :originalTitle="serie.original_name"
          :id="serie.id"
          :language="serie.original_language"
          :vote="serie.vote_average"
          :imgPath="serie.poster_path"
          :overview="serie.overview"/>
    </div>

  </div>
</template>

<script>
import Card from '../components/Card.vue'

export default {
    name: "Main",

    props: {
        filmList: Array,
        serieList: Array,
        filmCast: Array //
    },

    components: {
    Card
  },
}

</script>

<style scoped lang="scss">

h4 {
  color: white;
}

</style>