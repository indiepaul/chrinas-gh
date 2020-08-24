
<template>
  <Layout>
    <Hero :headerImg="$page.home.header_image"/>
    <div class="shade full">
      <h1 class="headline">About Chrina's</h1>
      <div class="cols">
        <g-image :src="$page.home.about_image" alt="Lounge" class="fl"/>
        <div class="excerpt">
          <div v-html="$page.home.content"></div>
          <g-link class="button" to="/reservations">{{$page.home.cta}}...</g-link>
        </div>
      </div>
    </div>
    <div class="full">
      <h1 class="headline">Feel at Home Away from Home</h1>
      <div class="posts tp">
        <div v-for="item in $page.posts.edges" :key="item.node.id" class="journal-post">
          <div class="container journal">
            <div class="img">
              <g-image :src="item.node.image" :alt="item.node.title" class="thumb"/>
            </div>
            <h2 class="journal-title">{{ item.node.title }}</h2>
          </div>
        </div>
      </div>
      <div class="container ct">
        <g-link class="button" to="/explore">Explore Chrina's...</g-link>
      </div>
    </div>
    <div
      class="cc full"
      :style="{ backgroundImage: 'linear-gradient(rgba(95, 83, 20, 0.6), rgba(255, 217, 0, 0.6)), url(\'' + $page.home.testimonial_image + '\')' }"
    >
      <h2 class="headline u">Testimonials</h2>
      <div class="quotes">
        <div class="qd" :style="quotePos()">
          <div v-for="quote in $page.home.testimonials" :key="quote.author" class="quote-con">
            <p class="quote">
              <i>{{ quote.body }}</i>
            </p>
            <p class="author">
              <b>{{ quote.author }}</b>
            </p>
          </div>
        </div>
      </div>
    </div>
    <!-- <CTA/> -->
    <!-- <pictures/> -->

    <!-- <LatestBlogs :blogs="$page.blogs.edges"/> -->
  </Layout>
</template>

<style scoped>
.quotes {
  text-align: center;
  overflow: hidden;
  position: relative;
  max-height: 300px;
}
.quote-con {
  padding-top: 4rem;
  height: 300px;
}
.quote,
.author {
  font-size: 1.5rem;
}
.quote:before,
.quote:after {
  content: '"';
}

.author:before {
  content: "- ";
}
.cc {
  color: white;
  background-attachment: fixed;
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
}
.excerpt {
  line-height: 1.7rem;
}
.full {
  margin-bottom: 2rem;
  padding: 2rem 6rem 4rem 6rem;
  min-height: 50vh;
  width: 100vw;
}
.shade {
  background-color: var(--color-base-1);
}
.ct {
  margin-top: 10px;
  margin-bottom: 20px;
}
.button {
  background-color: var(--theme-color);
  padding: 15px;
  text-decoration: none;
  font-weight: 500;
}
.button:hover {
  opacity: 0.6;
}

@media (max-width: 560px) {
  .cc {
    background-attachment: initial;
  }
  .full {
    padding: 2rem 1rem 4rem 1rem;
  }
}
</style>

<script>
import Hero from "@/components/Hero";
import LatestBlogs from "@/components/LatestBlogs";
import { setInterval } from "timers";

// i) Would it possible to adopt the presentation set up of www.baronscarhire.com, so that the opening page has the section links very visible and the picture of Chrina's is smaller ? I will send you a flyer which has a picture which you can adapt for the home page. I think is easier to see sections with a smaller picture rather than the one that feels the whole page.

// (iv) I am attaching the House Rules.  This can be added similar to the way the terms of contract appear on the Baron's website with four sub sections appearing on the main page.
// linear-gradient(rgba(237, 209, 50, 0.6), rgba(237, 209, 50, 0.6)),
export default {
  components: {
    Hero,
    LatestBlogs
  },
  data() {
    return {
      i: 0
    };
  },
  mounted() {
    if (this.$page.home.testimonials.length > 1) {
      var that = this;
      setInterval(function() {
        that.i++;
        if (that.i >= that.$page.home.testimonials.length) {
          that.i = 0;
        }
      }, 5000);
    }
  },
  methods: {
    quotePos() {
      return {
        transition: "transform 0.5s ease",
        transform: "translateY(" + this.i * -300 + "px)"
      };
    }
  }
};
</script>
<page-query>
query Posts {
  posts: allExplorePost {
    edges {
      node {
        id
        image
        path
        title
        content
      }
    }
  },
  home(path:"/data/home/"){
    header_image
  	about_image
    about_heading
    cta
    testimonials{
      author
      body
    }
    testimonial_image
    content
  }
}
</page-query>