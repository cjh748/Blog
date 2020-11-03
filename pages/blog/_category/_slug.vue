<template>
    <div>
      <div class="blog-post__title">
        <h1 class="blog-post__title-text">{{this.post.data.title}}</h1>
        <span>{{this.post.data.author.first_name}} {{ this.post.data.author.last_name }} &bull;</span>
        
        <span>{{formatDate(this.post.data.created)}}</span>
        <span>{{this.post.data}}</span>
      </div>
      

        <!-- <div v-html="this.post"></div> -->
    </div>
</template>

<script lang="js">
import moment from 'moment';
import { butter } from '~/plugins/buttercms';

export default {
  name: 'blog-post',
  data() {
    return {
      post: {
        data: {
          author: {}
        },
        meta: {}
      },  
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
  watch: {
    $route(to, from) {
      this.getPost();
    }
  },
  created() {
    this.getPost();
  }
}
</script>