<template>
  <div>
    <div class="card">
      <div class="card-image">
        <figure class="image is-4by3">
          <img
            class="img-pokemon"
            :src="pokemon.frontImage"
            :alt="pokemon.name"
          />
        </figure>
      </div>
      <div class="card-content">
        <div class="content">
          <p>N° {{ num }}</p>
          <p class="title is-3">{{ name | upperCaseFirstLetter }}</p>
          <div class="row-types">
            <p :key="i" v-for="(type, i) in pokemon.types">
              {{ type.name | upperCaseFirstLetter }}
            </p>
          </div>
          <button class="button is-primary" @click="modalActive = true">
            Ver detalhes
            <i class="fas fa-location-arrow pl-2"></i>
          </button>
        </div>
      </div>
    </div>
    <b-modal v-model="modalActive">
      <div class="card">{{ pokemon }}</div>
    </b-modal>
  </div>
</template>

<script lang="ts">
import Vue from "vue";
import axios from "axios";

export default Vue.extend({
  name: "Pokemon",
  props: {
    num: { type: Number, required: false },
    name: { type: String, required: false },
    url: { type: String, required: false },
  },
  data() {
    return {
      modalActive: false,
      pokemon: {
        types: [],
        frontImage: "",
        backImage: "",
      },
    };
  },
  async created() {
    axios.get(this.url).then((res) => {
      this.pokemon.frontImage = res.data.sprites.front_default;
      this.pokemon.backImage = res.data.sprites.back_default;

      res.data.types.forEach((data: any) => {
        this.$data.pokemon.types.push({
          name: data.type.name,
        });
      });
      console.log(res.data);
    });
  },
  filters: {
    upperCaseFirstLetter: (value: string) => {
      let nameFormatted = value[0].toUpperCase() + value.slice(1);
      return nameFormatted;
    },
  },
});
</script>

<style lang="scss" scoped>
.card {
  border-radius: 15px;

  .img-pokemon {
    image-rendering: -moz-crisp-edges;
    image-rendering: -webkit-crisp-edges;
    image-rendering: pixelated;
    image-rendering: crisp-edges;
  }

  .row-types {
    display: flex;

    p {
      margin: 0 1rem 1rem 0;
    }
  }
}
</style>
