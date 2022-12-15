<script setup>
import axios from 'axios';
import { ref } from 'vue';
import { RouterLink } from 'vue-router';

const pokemons = ref([]);

const getData = async () => {
    try {
        const { data } = await axios('https://pokeapi.co/api/v2/pokemon')
        pokemons.value = data.results
    } catch (error) {
        console.log(error)
    }
};
getData();
</script>

<template>
    <ul class="bg-dark mt-5 rounded shadow-lg list-group">
        <li class="list-group-item list-group-item-action" v-for="(pokemon, index) in pokemons" :key="index">
            <router-link :to="`/pokemons/${pokemon.name}`">
                {{ pokemon.name }}
            </router-link>
        </li>
    </ul>
</template>