<template>
  <div class="hero">
    <div class="contain">
      <h1 class="hero-title" v-html="settings.hero_title"/>
      <h2 class="hero-subtitle" v-html="settings.hero_subtitle"/>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      settings: require("../../data/theme.json")
    };
  }
};
</script>

<style>
.contain {
  width: 480px;
  max-width: 100%;
  margin: auto;
}
.hero {
  position: absolute;
  top: 50%;
  text-align: center;
  /* width: 480px; */
  width: 100%;
  margin: 0 auto;
  padding-top: 4rem;
}

.hero-title {
  font-size: 3rem;
  font-weight: 700;
  padding: 0;
  margin: 0 0 2rem 0;
  color: white;
}
.hero-title p,
.hero-subtitle p {
  margin: 0;
  padding: 0;
}
.hero-subtitle {
  font-weight: 400;
  color: white;
  line-height: 1.68;
  padding: 0;
  margin: 0;
}

@media (max-width: 560px) {
  .hero {
    margin-bottom: 1rem;
    top: -3em;
  }
  .hero-title {
    font-size: 1.8rem;
  }
  .hero-subtitle {
    line-height: 0.3;
  }
}
</style>
