<template>
  <div class="search_bar">
    <input v-model="search" type="text" />
    <button @click="$emit('searchMovies', search)">Search</button>
  </div>
  <!--./searchBar -->
</template>

<script>
export default {
  data() {
    return {
      search: "",
    };
  },
  methods: {
    searchMovies(digitText) {
      console.log(digitText);
    },
  },
};
</script>

<style lang="scss">
.logo {
  display: flex;
  justify-content: space-between;
  input {
    margin-right: 1rem;
  }
}
input {
  width: 300px;
  height: 50px;
  padding: 10px;
  border-radius: 10px;
}
button {
  height: 50px;
  width: 100px;
  padding: 10px;
  border-radius: 10px;
  font-size: 18px;
}
button:hover {
  background: url(../assets/img/fire.gif);
  object-fit: cover;
  background-position: center;
  background-repeat: no-repeat;
  transition: all 1s;
  color: white;
}
</style>