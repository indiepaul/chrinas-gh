<template>
  <div class="sliders">
    <carousel :controls-visible="true" :display="3" :height="500" :width="900">
      <slide v-for="(slider, index) in sliders" :index="index" :key="index">
        <div class="slider">
          <g-image :src="slider.node.image" :alt="slider.node.title" class="thumbnail"/>
          <div class="container">
            <h2 class="title">{{ slider.node.title }}</h2>
          </div>
        </div>
      </slide>
    </carousel>
  </div>
</template>

<style scoped>
.thumbnail {
  width: 90vh;
}
.sliders .container {
  position: relative;
  background-color: rgba(0, 0, 0, 0.3);
  top: -13rem;
  padding: 1rem 3rem;
  text-align: center;
}
.title {
  color: var(--color-base-1);
}
@media (max-width: 560px) {
  .sliders .container {
    padding: 0.3rem 1rem;
    top: -7em;
  }
}
</style>

<script>
import Hero from "@/components/Hero";
let Carousel3d;
if (process.isClient) {
  Carousel3d = require("vue-carousel-3d");
} else {
  let Vue = require("vue");
  Carousel3d = {
    Carousel3d: Vue.component("carousel-3d", {
      props: [""],
      template: "<div />"
    }),
    Slide: Vue.component("slider", {
      props: [""],
      template: "<div />"
    })
  };
}

export default {
  props: {
    sliders: {
      type: Array,
      required: true
    }
  },
  data() {
    return {
      slides: 7
    };
  },
  components: {
    Hero,
    carousel: Carousel3d.Carousel3d,
    slide: Carousel3d.Slide
  }
};
</script>
