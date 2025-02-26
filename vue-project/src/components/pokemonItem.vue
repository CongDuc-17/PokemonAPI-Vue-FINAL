<script setup>
import { ref, onMounted } from "vue";
import { useRouter } from "vue-router";

const props = defineProps(["url"]);
defineEmits(["select-pokemon"]);
const router = useRouter();
async function cFetch(URL) {
  const response = await fetch(URL);
  return await response.json();
}
const pokemon = ref({});
const pokemon__desc = ref({});
cFetch(props.url).then((data) => {
  pokemon.value = data;
});
async function fetchPokemon() {
  pokemon.value = await cFetch(props.url);

  const speciesData = await cFetch(
    `https://pokeapi.co/api/v2/pokemon-species/${pokemon.value.id}/`
  );
  pokemon__desc.value =
    speciesData.flavor_text_entries
      .find((entry) => entry.language.name === "en")
      ?.flavor_text.replace(/[\n\f]/g, " ") || "";
}

function viewPokemonDetail() {
  sessionStorage.setItem("selectedPokemon", JSON.stringify(pokemon.value));
  router.push("/" + pokemon.value.name);
}
onMounted(fetchPokemon);
</script>
<template>
  <div class="item" @click="viewPokemonDetail">
    <div class="item__id">#{{ pokemon.id }}</div>
    <div
      class="item__image"
      :style="`background-image: url('https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${pokemon.id}.png');`"
    ></div>
    <div class="item__name">{{ pokemon.name }}</div>
    <div class="type">
      <span
        v-for="type in pokemon.types"
        :key="type.type.name"
        class="type__name"
        :class="type.type.name"
      >
        {{ type.type.name }}
      </span>
    </div>
  </div>
</template>
<style>
.item {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.normal {
  background-color: #a8a77a;
}

.fighting {
  background-color: #c22e28;
}

.flying {
  background-color: #a98ff3;
}

.poison {
  background-color: #a33ea1;
}

.ground {
  background-color: #e2bf65;
}

.rock {
  background-color: #b6a136;
}

.bug {
  background-color: #a6b91a;
}

.ghost {
  background-color: #735797;
}

.steel {
  background-color: #b7b7ce;
}

.fire {
  background-color: #ff421c;
}

.water {
  background-color: #6390f0;
}

.grass {
  background-color: #78cd54;
}

.electric {
  background-color: #f7d02c;
}

.psychic {
  background-color: #f95587;
}

.ice {
  background-color: #96d9d6;
}

.dragon {
  background-color: #6f35fc;
}

.dark {
  background-color: #705746;
}

.fairy {
  background-color: #d685ad;
}

.unknow {
  background-color: #68a090;
}

.shadow {
  background-color: #735797;
}
</style>
