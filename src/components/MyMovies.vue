<template>
  <div class="container">
    <div class="search_bar">
      <input v-model="search" type="text" />
      <button @click="searchMovie()">Search movie</button>
    </div>
    <div class="movie" v-for="movie in movies" :key="movie.id">
      <p>{{ movie.title }}</p>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      search: "",
      api_url:
        "https://api.themoviedb.org/3/search/movie?api_key=2c70cf7212141e650767768ea94e23e6&language=en-US&query=matrix&page=1&include_adult=false",
      movies: [],
    };
  },
  methods: {
    searchMovie() {
      // console.log('cliccato sul button')
      console.log(this.search);
    },
  },
  mounted() {
    axios
      .get(this.api_url)
      .then((response) => {
        console.log(response);
        this.movies = response.data.results;
        console.log(this.movies);
      })
      .catch((error) => {
        console.log(error);
      });
  },
};
</script>

<style lang="scss">
.container {
  max-width: 1200px;
  margin: 2rem auto;
  .search_bar {
    display: flex;
    justify-content: center;
    input {
      margin-right: 1rem;
    }
  }
}
</style>