<template>
  <div class="container">
    <Logo />
    <div class="columns is-multiline">
      <div class="column is-one-third" :key="i" v-for="(poke, i) in pokemons">
        <Pokemon
          :pokemonData="poke"
          :name="poke.name"
          :url="poke.url"
          :num="i + 1"
        />
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from "vue";
import axios from "axios";
import Logo from "@/components/Logo.vue";
import Pokemon from "@/components/Pokemon.vue";

export default Vue.extend({
  name: "Home",
  components: { Logo, Pokemon },
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
