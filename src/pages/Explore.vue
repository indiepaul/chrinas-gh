<template>
  <Layout>
    <div class="container">
      <div class="journal-hero">
        <h1 class="journal-header">Explore Chrina's</h1>
      </div>
    </div>
    <div class="posts">
      <div v-for="item in $page.posts.edges" :key="item.node.id" :class="selected(item.node.id)">
        <div class="container journal" @click="change(item)">
          <div class="img">
            <g-image :src="item.node.image" :alt="item.node.title" class="thumbnail"/>
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
}
</page-query>

<script>
export default {
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
      return "journal-post";
    }
  },
  mounted() {
    this.post = this.$page.posts.edges[0];
  }
};
</script>

<style scoped>
.container.journal {
  max-width: 720px;
}
.img {
  height: 80px;
}
.journal-hero {
  padding: 4rem 0;
  text-align: center;
  color: var(--color-base-1);
}
.journal-header {
  font-size: 3rem;
  font-weight: 700;
  padding: 0;
  margin: 0;
}
.posts {
  display: flex;
}
.journal-post {
  display: block;
  padding: 1rem 0;
  width: 20%;
  text-decoration: none;
  transition: background 0.5s ease;
}
.journal-post > * {
  transition: transform 0.5s ease;
}
.journal-post:hover,
.active {
  background-color: var(--color-base-1);
}
.journal-post:hover > *,
.active {
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
.thumbnail {
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
  .journal-hero {
    padding: 1rem 0;
  }
  .journal-header {
    font-size: 3rem;
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
}
</style>
