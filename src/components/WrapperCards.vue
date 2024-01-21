<script setup>
import { defineProps  } from 'vue';
import CardPokemon from './CardPokemon.vue';
const pokemons = defineProps(['pokemonList']);
</script>

<template>
        <ul class="c-list" v-if="pokemonList.length > 0">
            <CardPokemon
            v-for="pokemon in pokemonList"
            :key="pokemon.name"
            :pokemon="pokemon"
            />
        </ul>
        <p v-else>
            No results
        </p>
</template>

<style lang="scss">
.c-list {
    display: grid;
    gap: 0.5rem;

    @media only screen and (min-width: 420px) {
        grid-template-columns: repeat(2, minmax(200px, 300px));
    }

    @media only screen and (min-width: 640px) {
        grid-template-columns: repeat(3, 1fr);
    }

    @media only screen and (min-width: 968px) {
        grid-template-columns: repeat(4, 1fr);
    }
}

</style>