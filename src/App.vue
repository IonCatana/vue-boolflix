<template>
  <div id="app">
    <MyMovies />
  </div>
</template>

<script>
import MyMovies from "./components/MyMovies.vue";
export default {
  name: "App",
  components: {
    MyMovies,
  },
};
</script>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
</style>
