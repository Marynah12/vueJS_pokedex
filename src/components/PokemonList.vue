<template>
  <div class="list">
    <article
      v-for="pokemon in pokemonsFiltered"
      v-bind:key="pokemon.name"
      v-on:click="showPokemonDetail(pokemon)"
    >
      <h3>{{ pokemon.name }}</h3>
      <img :src="URLImage + pokemon.name + '.png'" />
    </article>
  </div>
</template>

<script>
import axios from "axios";
import lodash from "lodash";
import conf from "../config/config.json";
export default {
  data: () => {
    return {
      pokemons: [],
      URLImage: conf.IMG_URL,
    };
  },
  props: {
    search: String,
  },
  computed: {
    pokemonsFiltered: function () {
      if (this.search === "") {
        return this.pokemons;
      }
      // Convertit la recherche en majuscule pour que l'utilisateur puisse rechercher en minuscule ou en majuscule
      let s = this.search.toUpperCase();
      return lodash.filter(this.pokemons, function (pokemon) {
        return lodash.includes(pokemon.name.toUpperCase(), s);
      });
    },
  },
  methods: {
    //  Fonction callback au clique d'un pokémon
    showPokemonDetail: function (pokemon) {
      // Envoie d'un événement au parent : Pokedex
      this.$emit("pokemonClicked", pokemon);
    },
  },
  beforeMount() {
    // Appel de l'api pour récuperer la liste des pokémons
    axios.get(conf.API_URL + "/pokemon").then((e) => {
      // Stockage de la data dans pokemons
      this.pokemons = e.data.results;
    });
  },
};
</script>

<style lang="scss" scoped>
.list {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
  grid-gap: 10px;
  width: 100%;
  max-width: 510px;
}
article {
  height: 150px;
  background-color: #efefef;
  text-align: center;
  text-transform: capitalize;
  border-radius: 5px;
  cursor: pointer;
  box-shadow: 0 15px 30px rgba(0, 0, 0, 0.2), 0 10px 10px rgba(0, 0, 0, 0.2);
}
h3 {
  margin: 0;
}
#scroll-trigger {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 150px;
  font-size: 2rem;
  color: #efefef;
}

img {
  width: 96px;
  height: 96px;
}
li {
  list-style: none;
}
</style>
