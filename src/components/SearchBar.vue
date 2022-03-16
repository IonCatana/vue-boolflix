<template>
  <div class="search_bar">
    <input v-model="search" type="text" />
    <button @click="$emit('searchMovies', search)">Search</button>
  </div>
  <!--./searchBar -->
</template>

<script>
export default {
  data () {
    return {
      search: ''
    }
  },
  methods: {
    searchMovies (digitText) {
      console.log(digitText)
    }
  }
}
</script>

<style lang="scss">
.logo {
    display: flex;
    justify-content: space-between;
    input {
      margin-right: 1rem;
    }
  }
</style>