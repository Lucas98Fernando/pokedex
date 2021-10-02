<template>
  <div>
    <div class="card">
      <div class="card-image" @mouseenter="toggleImg()" @mouseout="toggleImg()">
        <figure class="image is-4by3">
          <img class="img-pokemon" :src="currentImg" :alt="name" />
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
          <!-- <button class="button is-primary" @click="modalActive = true">
            Ver detalhes
            <i class="fas fa-location-arrow pl-2"></i>
          </button> -->
        </div>
      </div>
    </div>
    <!-- <b-modal v-model="modalActive">
      <div class="card py-4">
        <div class="has-text-centered">
          <h3 class="is-size-3">{{ name | upperCaseFirstLetter }}</h3>
        </div>
        <Carousel :carousels="carousels" />
      </div>
    </b-modal> -->
  </div>
</template>

<script lang="ts">
import Vue from "vue";
import axios from "axios";
// import Carousel from "@/components/Carousel.vue";

export default Vue.extend({
  name: "Pokemon",
  components: {
    //Carousel
  },
  props: {
    num: { type: Number, required: false },
    name: { type: String, required: false },
    url: { type: String, required: false },
  },
  data() {
    return {
      isFront: true,
      currentImg: "",
      // modalActive: false,
      pokemon: {
        types: [],
        frontImage: "",
        backImage: "",
      },
      // colorText: "",
      carousels: [],
    };
  },
  async created() {
    axios.get(this.url).then((res) => {
      this.pokemon.frontImage = res.data.sprites.front_default;
      this.pokemon.backImage = res.data.sprites.back_default;
      this.currentImg = this.pokemon.frontImage;

      res.data.types.forEach((data: any) => {
        this.$data.pokemon.types.push({
          name: data.type.name,
        });
      });

      // const allTypes = this.pokemon.types;

      // const colorType = (type: any) => {
      //   if (type.name == "grass") {
      //     return (this.colorText = "has-text-success");
      //   } else if (type.name == "poison") {
      //     return (this.colorText = "has-text-danger");
      //   }
      // };
      // const result = allTypes.find(colorType);
      // console.log(result);

      // Todos os spites do pokémon
      const allSprites = res.data.sprites;
      // Pegando somente os valores do objeto dos spites e removendo os valores nulo
      const spritesValues = Object.values(allSprites).filter((n) => n);
      // Inserindo no array do carousel somente as URL's dos sprites
      this.$data.carousels = spritesValues;
      // console.log(this.carousels);
      // console.log(res.data);
    });
    console.log(this.pokemon.types);
  },
  filters: {
    upperCaseFirstLetter: (value: string) => {
      let nameFormatted = value[0].toUpperCase() + value.slice(1);
      return nameFormatted;
    },
  },
  methods: {
    toggleImg() {
      if (this.isFront) {
        this.isFront = false;
        this.currentImg = this.pokemon.backImage;
      } else {
        this.isFront = true;
        this.currentImg = this.pokemon.frontImage;
      }
    },
  },
});
</script>

<style lang="scss" scoped>
.card {
  border-radius: 15px;
  max-width: 500px;
  margin: 0 auto;
  transition: 0.3s ease-in-out;

  &:hover {
    transform: scale(1.05);
  }

  .card-image {
    cursor: pointer;
  }

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
