<template>
  <b-carousel :pause-hover="false">
    <b-carousel-item v-for="(carousel, i) in carousels" :key="i">
      <div class="hero-body has-text-centered">
        <img :src="carousel" width="120px" />
      </div>
    </b-carousel-item>
  </b-carousel>
</template>

<script lang="ts">
import Vue from "vue";
export default Vue.extend({
  name: "Carousel",
  props: {
    carousels: {
      type: Array,
    },
  },
});
</script>
