<template>
  <div class="container">
    <div class="search_bar">
      <input type="text" />
      <button>Search movie</button>
    </div>
  </div>
</template>

<script>
export default {};
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