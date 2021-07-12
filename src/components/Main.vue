<template>
  <div class="hello">
    <h2>{{ msg }}</h2>

    <ul>
      <li>Titolo: {{ title }}</li> 
      <li>Titolo originale: {{ originalTitle }}</li>
      <li>Lingua originale: {{ language }}</li>
      <li>Voto medio: {{ vote }}</li>
    </ul>
    
  </div>
</template>

<script>

export default {
  name: 'Main',
  props: {
    msg: String,
    title: String,
    originalTitle: String,
    language: String,
    vote: Number,
  },
}
</script>

<style scoped lang="scss">

</style>
