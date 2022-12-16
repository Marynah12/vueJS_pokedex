<template>
  <div class="searchbar">
    <input type="text" v-model="search" placeholder="Search a pokemon" />
  </div>
</template>

<script>
export default {
  data: () => {
    return {
      search: "",
    };
  },
  watch: {
    search: function () {
      // Envoie d'un événement au parent : Pokedex
      this.$emit("searchPokemonEmit", this.search);
    },
  },
};
</script>

<style scoped>
.searchbar {
  position: relative;
  width: 100%;
  max-width: 510px;
  padding-bottom: 20px;
}
input {
  border: none;
  outline: none;
  border-radius: 5px;
  padding: 10px 40px 10px 10px;
  width: calc(100% - 50px);
  font-size: 1rem;
  box-shadow: 0 15px 30px rgba(0, 0, 0, 0.2), 0 10px 10px rgba(0, 0, 0, 0.2);
}
</style>
