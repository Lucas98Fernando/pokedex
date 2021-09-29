<template>
  <div>
    <div class="card">
      <div class="card-image">
        <figure class="image is-4by3">
          <img :src="pokemon.frontImage" alt="Placeholder image" />
        </figure>
      </div>
      <div class="card-content">
        <div class="content">
          <p>N° {{ num }}</p>
          <p class="title is-4">{{ name | upperCaseFirstLetter }}</p>
          <b-button
            label="Ver detalhes"
            type="is-primary"
            icon-right="link"
            @click="modalActive = true"
          />
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
        type: "",
        frontImage: "",
        backImage: "",
      },
    };
  },
  created() {
    axios.get(this.url).then((res) => {
      this.pokemon.type = res.data.types[0].type.name;
      this.pokemon.frontImage = res.data.sprites.front_default;
      this.pokemon.backImage = res.data.sprites.back_default;
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
}
</style>
