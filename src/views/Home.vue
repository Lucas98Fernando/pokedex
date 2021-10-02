<template>
  <div class="container">
    <Logo />
    <b-field
      message="Encontre o seu pokémon preferido"
      class="has-text-white mb-4"
    >
      <b-input
        v-model="search"
        placeholder="Pesquisar um pokémon..."
        expanded
        icon="magnify"
        rounded
      ></b-input>
      <p class="control">
        <b-button
          id="searchBtn"
          label="Pesquisar"
          type="is-warning"
          rounded
          @click="searchPokemons()"
        />
      </p>
    </b-field>
    <div class="columns is-multiline">
      <div
        class="column is-one-third"
        v-for="(poke, i) in filteredPokemons"
        :key="poke.url"
      >
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
      filteredPokemons: [],
      search: "",
    };
  },
  created() {
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=151").then((resp) => {
      this.pokemons = resp.data.results;
      this.filteredPokemons = resp.data.results;
      // console.log(resp.data.results);
    });
  },
  methods: {
    searchPokemons: function () {
      // Resetando a lista
      this.filteredPokemons = this.pokemons;
      if (this.search == "" || this.search == " ") {
        this.filteredPokemons = this.pokemons;
      } else {
        // eslint-disable-next-line @typescript-eslint/no-explicit-any
        this.filteredPokemons = this.pokemons.filter((pokemon: any) =>
          pokemon.name.match(this.search.toLocaleLowerCase())
        );
      }
    },
  },
  computed: {
    // searchResult: function (): any {
    //   if (this.search == "" || this.search == " ") {
    //     return this.pokemons;
    //   } else {
    //     return this.pokemons.filter(
    //       (pokemon: any) => pokemon.name == this.search
    //     );
    //   }
    // },
  },
});
</script>
