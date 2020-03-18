<template>
  <Layout>
    <div class="container">
      <div class="hero">
        <h1 class="hero-title">House Rules</h1>
      </div>
    </div>
    <div class="posts">
      <div v-for="item in $page.rules.edges" :key="item.node.id" :class="selected(item.node.id)">
        <div class="container journal" @click="change(item)">
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
query Rules {
	rules: allHouseRules(sortBy:"id", order: ASC){
    edges{
      node{
        id
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
      return "journal-post click";
    }
  },
  mounted() {
    this.post = this.$page.rules.edges[0];
  }
};
</script>
