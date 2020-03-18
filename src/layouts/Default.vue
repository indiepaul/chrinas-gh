<template>
  <div class="layout" :class="{ 'sticky-header': $route.path === '/' }">
    <Header/>
    <slot/>
    <Footer/>
  </div>
</template>

<script>
import Header from "@/components/Header";
import Footer from "@/components/Footer";

export default {
  components: {
    Header,
    Footer
  }
};
</script>


<style>
* {
  box-sizing: border-box;
}

body {
  --color-base: rgb(255, 255, 255);
  --theme-color: #edd132;
  --color-base-1: rgb(243, 243, 243);
  --color-contrast: rgb(0, 0, 0);
  --color-contrast-1: rgb(43, 43, 43);
  font-family: -apple-system, system-ui, BlinkMacSystemFont, "Segoe UI", Roboto,
    "Helvetica Neue", Arial, sans-serif;
  margin: 0;
  padding: 0;
  font-weight: 300;
  font-size: 16px;
  background: var(--color-base);
  color: var(--color-contrast);
  transition: background 0.5s ease;
}

body.dark {
  --color-base: rgb(0, 0, 0);
  --color-base-1: rgb(43, 43, 43);
  --color-contrast: rgb(255, 255, 255);
  --color-contrast-1: rgb(243, 243, 243);
}

h1 {
  letter-spacing: -0.01em;
}
h1:after {
  content: "";
  width: 100px;
  margin-top: 10px;
  margin-left: auto;
  margin-right: auto;
  display: block;
  height: 5px;
  background-color: var(--theme-color);
  bottom: -15px;
}
h2.u:after {
  content: "";
  width: 75px;
  margin-top: 10px;
  margin-left: auto;
  margin-right: auto;
  display: block;
  height: 3px;
  background-color: var(--theme-color);
  bottom: -15px;
}

.headline {
  text-align: center;
}

.layout {
  padding: 0;
}
.layout.sticky-header {
  padding: 4rem 0 0 0;
}

@media (max-width: 644px) {
  .layout.sticky-header {
    padding: 0rem 0 0 0;
  }
}
.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 2rem;
}
.hero {
  padding: 4rem 0;
  text-align: center;
  color: var(--color-base-1);
}
.hero-title {
  font-size: 3rem;
  font-weight: 700;
  padding: 0;
  margin: 0;
}

@media (max-width: 560px) {
  .hero {
    padding: 1rem 0;
  }
  .hero-title {
    font-size: 3rem;
  }
}
@media (max-width: 860px) {
  .container {
    padding: 0 1rem;
  }
}
@media (min-width: 860px) {
  .container {
    padding: 0 6rem;
  }
}

a {
  color: inherit;
}

img {
  max-width: 100%;
}

.label {
  display: block;
  font-weight: 700;
  margin-bottom: 0.5rem;
}

.container.journal {
  max-width: 720px;
}
.img {
  height: 80px;
  display: grid;
}
.img img {
  margin: auto;
}

.posts {
  display: flex;
}
.journal-post {
  display: block;
  padding: 1rem 0;
  width: 20%;
  text-decoration: none;
  text-align: center;
  transition: transform 0.5s ease;
}
.journal-post > * {
  transition: background 0.5s ease;
}
.journal-post.click:hover {
  background-color: var(--color-base-1);
  cursor: pointer;
}
.journal-post.active {
  background-color: var(--color-base-1);
  transform: translateY(-1rem);
}
.journal-post h1,
.journal-post h2 {
  margin: 0;
  padding: 0;
}
.journal-title {
  font-size: 2rem;
  color: var(--color-contrast);
}
.journal-excerpt {
  color: var(--color-contrast-1);
}
.thumb {
  float: left;
  max-width: 50px;
  margin-right: 20px;
}

@media (max-width: 560px) {
  .container.journal {
    padding: 0;
  }
  .img {
    padding: 1rem;
  }
  .journal-title {
    font-size: 0.9rem;
    text-align: center;
    font-weight: normal;
  }
  .journal-post {
    padding: 2rem 0;
  }
}
@media (min-width: 560px) {
  .journal-title {
    font-size: 1rem;
  }
  .journal-post {
    padding: 2rem 0;
  }
}

@media (min-width: 860px) {
  .journal-title {
    font-size: 1rem;
  }
  .journal-post {
    padding: 2rem 0;
  }
  .fl {
    max-width: 50%;
    margin-right: 2rem;
  }
  .cols {
    display: flex;
  }
}

.cols img:hover {
}
.tp {
  padding-top: 2rem;
}
</style>
