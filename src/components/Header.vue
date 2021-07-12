<template>
  <div class="header">
    <div class="title">
      <h1>{{ msg }}</h1>
    </div>

    <div class="search">
      <input type="text">
      <button>Search</button>
      <button>Reset</button>
    </div>

  </div>
</template>

<script>
export default {
  name: 'Header',
  props: {
    msg: String
  },

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
