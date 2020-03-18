<template>
  <Layout>
    <Slider :sliders="$page.sliders.edges"/>

    <div class="posts">
      <div v-for="item in $page.posts.edges" :key="item.node.id" :class="selected(item.node.id)">
        <div class="container journal" @click="change(item)">
          <div class="img">
            <g-image :src="item.node.image" :alt="item.node.title" class="thumb"/>
          </div>
          <h2 class="journal-title">{{ item.node.title }}</h2>
        </div>
      </div>
    </div>
    <div class="container">
      <div class="journal-excerpt" v-html="post.node.content"/>
    </div>
  </Layout>
</template>

<page-query>
query Explore {
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
  }
  sliders: allSlider(sortBy: "position", order: ASC){
    edges {
      node {
        id
        position
        title
        image
      }
    }
  }
}
</page-query>

<script>
import Slider from "@/components/Slider";
export default {
  components: {
    Slider
  },
  data() {
    return {
      post: {
        node: {
          id: "",
          content: ""
        }
      }
    };
  },
  methods: {
    change(post) {
      this.post = post;
    },
    selected(id) {
      if (this.post.node.id == id) return "journal-post active";
      return "journal-post click";
    }
  },
  mounted() {
    this.post = this.$page.posts.edges[0];
  }
};
</script>
