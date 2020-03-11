<template>
  <Layout>
    <Slider :sliders="$page.sliders.edges"/>
    <LatestBlogs :blogs="$page.blogs.edges"/>
  </Layout>
</template>

<page-query>
query Posts {
	sliders: allSlider(sortBy: "position", order: ASC){
    edges {
      node {
        id
        position
        title
        image
      }
    }
  },
  blogs: allBlogPost (perPage: 4) {
    edges {
      node {
        id
        path
        title
      }
    }
  }
}
</page-query>

<script>
import Slider from "@/components/Slider";
import LatestBlogs from "@/components/LatestBlogs";

export default {
  components: {
    Slider,
    LatestBlogs
  }
};
</script>
