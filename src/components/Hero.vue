<template>
  <div class="home" :style="{ backgroundImage: 'url(\'' +headerImg+'\')' }">
    <div class="contain">
      <h1 class="home-title" v-html="settings.hero_title"/>
      <h2 class="home-subtitle" v-html="settings.hero_subtitle"/>
    </div>
  </div>
</template>

<script>
export default {
  props:{
    headerImg: {
      type: String,
      required: true
    }
  },
  data() {
    return {
      settings: require("../../data/theme.json")
    };
  }
};
</script>

<style scoped>
.contain {
  width: 480px;
  max-width: 100%;
  margin: auto;
  text-align: center;
  vertical-align: center;
}
.home {
  display: flex;
  background-attachment: fixed;
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
  height: 75vh;
  margin-top: auto;
  margin-bottom: auto;

  /* padding-top: 4rem; */
}

.home-title {
  font-size: 3rem;
  font-weight: 700;
  padding: 0;
  margin: 0 0 2rem 0;
  color: white;
}
.home-title p,
.home-subtitle p {
  margin: 0;
  padding: 0;
}
.home-subtitle {
  font-weight: 400;
  width: 350px;
  margin-right: auto;
  margin-left: auto;
  color: white;
  line-height: 1.68;
  padding: 0;
}

@media (max-width: 560px) {
  .home {
    background-attachment: initial;
    top: -3em;
    height: 50vh;
  }
  .home-title {
    font-size: 1.8rem;
  }
  .home-subtitle {
    line-height: 2.3rem;
  }
}
</style>
