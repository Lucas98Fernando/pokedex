<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png" />
    <div :key="i" v-for="(poke, i) in pokemons">
      <Pokemon :name="poke.name" :url="poke.url" :num="i + 1" />
    </div>
  </div>
</template>

<script lang="ts">
import Vue from "vue";
import axios from "axios";
import Pokemon from "@/components/Pokemon.vue";

export default Vue.extend({
  name: "Home",
  components: { Pokemon },
  data() {
    return {
      pokemons: [],
    };
  },
  created() {
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=151").then((resp) => {
      this.pokemons = resp.data.results;
      console.log(resp.data.results);
    });
  },
});
</script>
