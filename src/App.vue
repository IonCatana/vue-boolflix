<template>
  <div id="app">
    <MyMovies/>
  </div>
</template>

<script>
import MyMovies from './components/MyMovies.vue'
export default {
  name: 'App',
  components: {
    MyMovies
  }
}
</script>

<style lang="scss">
@import '../node_modules/@fortawesome/fontawesome-free/css/all.css';
@import './assets/scss/variables.scss';
@import './assets/scss/common.scss';

body {
  background-color: #434343;  
}
.container {
  max-width: 1200px;
  margin: auto;
}
</style>
