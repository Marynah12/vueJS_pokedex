<template>
  <div class="container">
    <!-- Appel et paramétrage des composants du pokedex -->
    <PokemonSearch v-on:searchPokemonEmit="setPokemonSearch" />
    <PokemonDetail
      v-if="visible"
      v-on:pokemonClosed="closePokemonDetail"
      :pokemonURL="this.pokemonURL"
    />
    <PokemonList
      v-on:pokemonClicked="showPokemonDetail"
      :search="this.search"
    />
  </div>
</template>

<script>
import PokemonDetail from "../components/PokemonDetail.vue";
import PokemonList from "../components/PokemonList.vue";
import PokemonSearch from "../components/PokemonSearch.vue";

export default {
  data: function () {
    return {
      visible: false,
      search: "",
    };
  },
  components: {
    PokemonDetail,
    PokemonList,
    PokemonSearch,
  },
  methods: {
    showPokemonDetail: function (pokemon) {
      this.pokemonURL = pokemon.url;
      this.visible = true;
    },
    closePokemonDetail: function () {
      this.visible = false;
    },
    setPokemonSearch: function (search) {
      this.search = search;
    },
  },
};
</script>

<style lang="scss" scoped>
.container {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  padding: 10px;
  width: calc(100% - 20px);
  min-height: calc(100vh - 20px);
  //background: radial-gradient(#ffbf0b, #e20000);

  font-family: "Acme", arial;
  font-size: 1rem;
  font-weight: normal;
}

h1 {
  color: #efefef;
}
</style>
