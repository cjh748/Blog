<template>
    <div class="blog-post">
      <div class="blog-post__hero" :style="{'background-image':`url(${this.post.data.featured_image})`}">
        <svg class="swoop-sprite" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="0 0 450 48">
          <path id="swoop-compact"  d="M0 0c71 31 177 47 320 48H0V0z" />
        </svg>
      </div>
      <div class="blog-post-content">
        <div class="blog-post-content__category">
          <h3>{{ this.post.category }}</h3>
        </div>
        <div class="blog-post-content__title">
          <h1 class="blog-post-content__title-text">{{this.post.data.title}}</h1>
          <div class="blog-post-content__title-credentials">
            <span>&bull; {{this.post.data.author.first_name}} {{ this.post.data.author.last_name }} &bull;</span>
            <span>{{formatDate(this.post.data.created)}} &bull;</span>
          </div>
        </div>
        <div v-html="this.post.data.body"></div>
      </div>
    </div>
</template>

<script lang="js">
import moment from 'moment';
import NavigationBar from '@/components/Shared/NavigationBar/NavigationBar';
import { butter } from '~/plugins/buttercms';

export default {
  name: 'blog-post',
  components: {
    NavigationBar
  },
  data() {
    return {
      post: {
        data: {
          author: {}
        },
        meta: {},
        category: ''
      },  
    }
  },
  head() {
    return {
      title: 'Blog | ' + this.post.data.title
    }
  },
  methods: {
    getPost() {
      butter.post
        .retrieve(this.$route.params.slug)
        .then((res) => {
          console.log('results data: ' + res.data)
          this.post = res.data;
      })
      .catch((res) => {
        console.log(res);
      })
    },
    formatDate(date) {
      return moment(String(date)).format('dddd, MMMM Do YYYY')
    }
  },
  async fetch() {
    butter.post
        .retrieve(this.$route.params.slug)
        .then((res) => {
          console.log('results data: ' + res.data)
          this.post = res.data;
          this.post.category = res.data.data.categories[0].name
      })
      .catch((res) => {
        console.log(res);
      })
  },
  watch: {
    // $route(to, from) {
    //   this.getPost();
    // }
  },
  created() {
    // this.getPost();
  }
}
</script>

<style lang="scss">
.blog-post {
  $root: &;

  &__hero {
    background-size: cover;
    background-position: center;
    height: 500px;
    position: relative;
    z-index: -1;

    svg {
      width: 100%;
      bottom: 0;
      position: absolute;

      path {
        fill: white;
      }
    }
  }

  &-content {
    padding: 2rem;
    padding-top: 0;

    &__category {
      letter-spacing: 8px;
      color: $color-grape;
      padding: 0.5rem;
      width: fit-content;
      background: $color-light-grey;
      border-radius: 16px;
      text-transform: uppercase;
    }

    &__title {
      margin: 2rem 0;

      &-text {
        color: $color-pacific;
        font-size: 48px;
        line-height: normal;
      }

      &-credentials {
        margin: 0.5rem  0 0.5rem 0.5rem;
        font-style: italic;
        font-size: small;
        font-weight: bold;
      }
    }
  }
}
</style>