<script setup>
import SearchPokemon from './components/SearchPokemon.vue'
import WrapperCards from './components/WrapperCards.vue'
import { onMounted, reactive } from "vue";
import { fetchData } from './utils/apiUtils';

let pokemons = reactive({ list: [] });
let filteredPokemons = reactive({ list: [] });

onMounted(async () => {  
  const data = await fetchData('https://pokeapi.co/api/v2/pokemon?limit=151&offset=0');
  pokemons.list = data.results;
  filteredPokemons.list = pokemons.list;
});

const handleSearch = (searchTerm) => {
  filteredPokemons.list = pokemons.list.filter(pokemon => pokemon.name.startsWith(searchTerm.toLowerCase()));
};

</script>

<template>
  <SearchPokemon @search="handleSearch" />
  <WrapperCards :pokemonList="filteredPokemons.list" />
</template>

<style lang="scss">
</style>
