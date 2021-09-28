<template>
  <div class="card">
    <div class="card-image">
      <figure class="image is-4by3">
        <img
          src="https://bulma.io/images/placeholders/1280x960.png"
          alt="Placeholder image"
        />
      </figure>
    </div>
    <div class="card-content">
      <div class="media">
        <div class="media-left">
          <p>{{ num }}</p>
        </div>
        <div class="media-content">
          <p class="title is-4">{{ name | upperCaseFirstLetter }}</p>
        </div>
      </div>
      <div class="content">
        <a :href="url">Ver detalhes</a>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from "vue";
export default Vue.extend({
  name: "Pokemon",
  props: {
    num: Number,
    name: String,
    url: String,
  },
  data() {
    return {
      pokemons: [],
    };
  },
  filters: {
    upperCaseFirstLetter: (value: string) => {
      let nameFormatted = value[0].toUpperCase() + value.slice(1);
      return nameFormatted;
    },
  },
});
</script>
