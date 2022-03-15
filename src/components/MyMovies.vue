<template>
  <div class="container">
    <div class="search_bar">
      <input v-model="search" type="text" />
      <button @click="searchMovie()">Search movie</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      search: "",
    };
  },
  methods: {
    searchMovie() {
      //console.log('cliccato sul button')
      console.log(this.search);
    },
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