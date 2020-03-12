<template>
  <Layout>
    <div class="blog">
      <div class="container blog-container">
        <div class="blog-header">
          <h1 v-html="$page.post.title" class="blog-title"/>
          <div class="blog-meta">
            <div class="blog-author">
              <span class="label">Author</span>
              <span class="author-name" v-text="$page.post.author"/>
            </div>
            <div class="blog-date">
              <span class="label">Date</span>
              <div v-text="$page.post.date"/>
            </div>
            <div class="blog-time">
              <span class="label">Time</span>
              <span>{{ $page.post.timeToRead }} min read</span>
            </div>
          </div>
        </div>

        <BlogContent :content="$page.post.content"/>
      </div>
    </div>
  </Layout>
</template>

<page-query>
query BlogPost ($path: String!) {
  post: blogPost (path: $path) {
    title
    author
    date (format: "D. MMMM YYYY")
    timeToRead
    content
  }
}
</page-query>

<script>
import BlogContent from "@/components/BlogContent";

export default {
  components: {
    BlogContent
  },
  metaInfo() {
    return {
      title: this.$page.post.title
    };
  }
};
</script>

<style scoped>
.blog-container {
  max-width: 840px;
}
.blog-header {
  padding: 2rem 0 4rem 0;
}
.blog-title {
  font-size: 4rem;
  margin: 0 0 4rem 0;
  padding: 0;
}
.blog-meta {
  display: flex;
  flex-wrap: wrap;
  font-size: 0.8rem;
}
.blog-meta > div {
  margin-right: 4rem;
}
.blog-meta > div:last-of-type {
  margin: 0;
}
</style>
