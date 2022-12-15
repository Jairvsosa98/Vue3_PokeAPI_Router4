<script setup>
import axios from 'axios';
import { ref, onMounted } from 'vue';
import { useRoute, useRouter } from 'vue-router'

const route = useRoute()
const router = useRouter()

const poke = ref({})

const tipoPokemon = ref([])

const back = () => {
    router.push('/pokemons')
}

const getData = async () => {
    try {
        const { data } = await axios(`https://pokeapi.co/api/v2/pokemon/${route.params.name}`);
        poke.value = data

        const tipoPokemon = poke.value.types;
        console.log(tipoPokemon)

    } catch (error) {
        console.log(error)
        poke.value = null
    }
};
getData();



</script>
<template>
    <div class="d-flex justify-content-center" v-if="poke">
        <div class="card mt-5" style="width: 20rem;">
            <img :src="poke.sprites?.front_default" class="card-img-top bg-dark" :alt="poke.name">
            <div class="card-body">
                <h5 class="card-title text-center text-uppercase">{{ $route.params.name }}<span
                        v-for="(tipo, index) in poke.types" :key="index" class="badge bg-info ms-1 me-1">
                        {{ tipo.type.name }}
                    </span></h5>
                <ul class="list-group list-group-flush">
                    <li class="list-group-item">Altura: {{ poke.height }}cm</li>
                    <li class="list-group-item">Peso: {{ poke.weight }}g</li>

                </ul>
                <button class="btn btn-outline-primary mt-2 " @click="back">Regresar</button>
            </div>
        </div>
    </div>
    <div class="position-relative" v-else>
        <div class="position-absolute top-0 start-50 translate-middle-x">
            <h2 class="bg-dark text-white text-center mt-5 rounded shadow-lg">Tu pokédex no ha encontrado este pokemon
            </h2>
            <button class="btn btn-outline-primary mt-2 text-center" @click="back">Regresar</button>
        </div>
    </div>

</template>