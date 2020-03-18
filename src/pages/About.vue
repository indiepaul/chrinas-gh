<template>
  <Layout>
    <div class="container">
      <div class="hero">
        <h1 class="hero-title">About Us</h1>
      </div>
    </div>
    <div class="container">
      <g-image :src="$page.about.image" alt="about image"/>
      <div class="journal-excerpt" v-html="$page.about.content"/>
    </div>
  </Layout>
</template>


<page-query>
query About {
  about(path:"/data/about/"){
  	image
    content
  }
}
</page-query>