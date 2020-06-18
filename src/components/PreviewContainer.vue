<template>
  <div>
    <div v-if="searchedPokemon != ''" class="search-preview">
      <router-link
        v-for="pokemon in searchedPokemon"
        :key="pokemon.id"
        :to="`/pokemon/${pokemon.name}`"
      >
        <PokemonPreview :name="pokemon.name" :img="pokemon.img" />
      </router-link>
    </div>
    <div class="preview-container">
      <router-link
        v-for="pokemon in pokemons"
        :key="pokemon.id"
        :to="`/pokemon/${pokemon.name}`"
      >
        <PokemonPreview :name="pokemon.name" :img="pokemon.img" />
      </router-link>
    </div>
  </div>
</template>

<script>
import PokemonPreview from './PokemonPreview';
export default {
  name: 'PreviewContainer',
  components: {
    PokemonPreview
  },
  data: function() {
    return {
      pokemons: [],
      searchedPokemon: []
    };
  },
  props: {
    filterValue: String
  },
  methods: {
    searchPokemon() {
      if (this.filterValue === '') {
        this.searchedPokemon = [];
      } else {
        this.searchedPokemon = this.pokemons.filter(item => {
          return (
            item.name.toLowerCase().indexOf(this.filterValue.toLowerCase()) >= 0
          );
        });
      }
    }
  },
  mounted: function() {
    console.log('fetched');
    fetch("https://pokeapi.co/api/v2/pokemon?limit=151'")
      .then(res => res.json())
      .then(data => {
        const urls = data.results.map(item => item.url);
        urls.forEach(url =>
          fetch(url)
            .then(res => res.json())
            .then(data => {
              this.pokemons.push({
                name: data.name,
                img: data.sprites.front_default
              });
            })
        );
      });
  }
};
</script>

<style>
.preview-container {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}
.search-preview {
  display: flex;
  justify-content: center;
  width: 80vw;
  margin-left: 10vw;
  flex-wrap: wrap;
  margin-bottom: 10vh;
}
</style>
