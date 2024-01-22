<script setup>
import { onMounted, reactive, defineProps } from "vue";
import { fetchData } from '../utils/apiUtils';
import defaultImage from '../assets/pokeball.svg';


const pokemon = defineProps(["pokemon"]);
let pokemonData = reactive({ list: { sprites: { front_default: '' } } });

onMounted(async () => { 
    const data = await fetchData(pokemon.pokemon.url);
    pokemonData.list = data;
});
</script>

<template>
    <li class="c-card">
        <figure class="c-card__figure">
            <img 
                :src="pokemonData.list.sprites.front_default || defaultImage" 
                :alt="pokemon.pokemon.name"
            >
        </figure>
        <div class="c-card__footer">
            <p class="c-card__text">{{ pokemon.pokemon.name }}</p>
            <p class="c-card__text">#{{ pokemonData.list.id || '00' }}</p>
        </div>
    </li>
</template>


<style lang="scss">
.c-card {
    background: white;
    border-radius: 2px;
    padding: 8px;
    box-shadow: -2px 4px 2px -2px rgba(0,0,0,0.1);


    &__figure {
        width: 96px;
        height: 96px;
        margin: 0 auto;

        img {
            height: 100%;
            width: 100%;
            object-fit: contain;
        }
    }

    &__footer {
        display: flex;
        justify-content: space-between;
    }

    &__text {
        font-size: 0.75rem;
        text-transform: capitalize;
    }
}
</style>