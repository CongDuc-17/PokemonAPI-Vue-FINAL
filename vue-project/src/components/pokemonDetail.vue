<script setup>
import { ref } from "vue";

defineProps(["pokemon", "pokemon_desc"]);
defineEmits(["back"]);
const typeColors = {
  grass: "#78cd54",
  poison: "#a33ea1",
  fire: "#ff421c",
  flying: "#a98ff3",
  water: "#6390f0",
  bug: "#a6b91a",
  normal: "#a8a77a",
  electric: "#f7d02c",
  ground: "#e2bf65",
  fairy: "#d685ad",
  fighting: "#c22e28",
  psychic: "#f95587",
  rock: "#f95587",
  ghost: "#735797",
  ice: "#96d9d6",
  dragon: "#6f35fc",
  dark: "#705746",
  steel: "#b7b7ce",
};

const statsPara = {
  hp: "HP",
  attack: "ATK",
  defense: "DEF",
  "special-attack": "SPA",
  "special-defense": "SPD",
  speed: "SPD",
};
const colorLabel = {
  hp: "#df2140",
  attack: "#ff994d",
  defense: "#eecd3d",
  "special-attack": "#85ddff",
  "special-defense": "#96da83",
  speed: "#96da83",
};
</script>

<template>
  <button @click="$emit('back')" class="btnBack">&larr;Back</button>
  <div class="container">
    <div
      class="item__image"
      :style="{
        backgroundImage: `url(
          'https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${pokemon.id}.png'
        )`,
      }"
    ></div>

    <div class="item__type">
      <span
        v-for="type in pokemon.types"
        :key="type.type.name"
        class="type_item"
        :class="type.type.name"
        :style="{ backgroundColor: typeColors[type.type.name] }"
      >
        {{ type.type.name }}
      </span>
    </div>
    <div class="item__name">
      {{ pokemon.name }}
    </div>
    <p class="item__desc">{{ pokemon_desc }}</p>
    <div class="item__hei-wei">
      <div>
        <h3>Height</h3>
        <div class="number">{{ pokemon.height }}</div>
      </div>
      <div>
        <h3>Weight</h3>
        <div class="number">{{ pokemon.weight }}</div>
      </div>
    </div>
    <h3 :style="{}">Abilities</h3>
    <div class="item__abilities">
      <div v-for="ability in pokemon.abilities" :key="ability.ability.name">
        <div class="abi">
          {{ ability.ability.name }}
        </div>
      </div>
    </div>
    <h3>Stats</h3>
    <div class="item__stats">
      <div v-for="stat in pokemon.stats" :key="stat.stat.name" class="stats">
        <div class="label" :style="{ backgroundColor: colorLabel[stat.stat.name] }">
          {{ statsPara[stat.stat.name] }}
        </div>
        <div>{{ stat.base_stat }}</div>
      </div>
    </div>
  </div>
</template>
<style>
.btnBack {
  display: block;
  position: fixed;
  top: 5%;
  left: 5%;
  border-radius: 30px;
  padding: 5px 10px;
  box-shadow: #63636333 0 4px 8px;
  z-index: 999;
}
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  max-width: 500px;
}
button {
  display: block;
}
.item__image {
  width: 200px;
  height: 200px;
  background-size: cover;
  background-position: center;
  margin-bottom: 5px;
}
.item__type {
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  gap: 10px;
  font-size: 13px;
  text-transform: capitalize;
  margin-bottom: 5px;
  span {
    width: 100%;
    padding: 3px 10px;
    border-radius: 7px;
  }
}
.item__name {
  text-transform: capitalize;
  font-size: 22.5px;
  font-weight: 800;
  margin-bottom: 5px;
}
.item__desc {
  font-size: 15px;
  text-align: center;
  margin-bottom: 5px;
}
.item__hei-wei {
  width: 100%;
  display: flex;
  justify-content: space-evenly;
  margin-bottom: 5px;
  div {
    display: flex;
    flex-direction: column;
    align-items: center;
  }
}
.number,
.abi {
  width: 100px;
  margin: 5px;
  padding: 2px;
  border-radius: 30px;
  background-color: #f6f8fc;
  text-align: center;
  text-transform: capitalize;
  margin-bottom: 5px;
}
.item__abilities {
  width: 100%;
  display: flex;
  justify-content: space-evenly;
  margin-bottom: 5px;
}
.item__stats {
  width: 100%;
  display: flex;
  justify-content: space-evenly;
  margin-bottom: 5px;
}
.stats {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin: 5px;
  padding: 5px;
  background-color: #f6f8fc;
  border-radius: 30px;
  box-shadow: #63636333 0 2px 8px;
  margin-bottom: 5px;
  .label {
    display: flex;
    justify-content: center;
    align-items: center;
    border-radius: 50%;
    width: 25px;
    height: 25px;
    font-size: 10px;
    font-weight: 700;
  }
}
</style>
