<template>
  <div>
    <div>
      <dynamic-graph />
      <animated-title v-if="categories.length > 0" :categories=categories></animated-title>
      <blog-carousel></blog-carousel>
    </div>
  </div>
</template>

<script>
import Vue from 'vue';
import Introduction from '@/components/Shared/Introduction/Introduction.vue';
import BlogCarousel from '@/components/Carousel/BlogCarousel.vue';
import AnimatedTitle from '@/components/AnimatedTitle/AnimatedTitle';
import DynamicGraph from '@/components/DynamicGraph/DynamicGraph';
import { butter } from '~/plugins/buttercms';

export default Vue.extend({
  components: {
    Introduction,
    BlogCarousel,
    AnimatedTitle,
    DynamicGraph
  },
  data() {
    return {
      page_title: 'Blog',
      posts: [],
      categories: []
    }
  },
  async fetch() {
    butter.post
      .list({
        page: 1,
        page_size: 10
      })
      .then((res) => {
        const x = res.data.data
        let categories = [];

        x.forEach((item) => {
          let category = item.categories[0].name;
          if (!this.categories.includes(category)) {
            this.categories.push(item.categories[0].name)
          }
        })
      })
  }
})
</script>

<style lang="scss">
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family:
    'Quicksand',
    'Source Sans Pro',
    -apple-system,
    BlinkMacSystemFont,
    'Segoe UI',
    Roboto,
    'Helvetica Neue',
    Arial,
    sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}

</style>
