<template>
    <div class="blog-list">
      <h1>Blogs by Category</h1>
        <!-- <input type="text" v-model="search" /> -->
        <select v-model="search">
          <option 
            v-for="(category, index) in this.categories" 
            :key="`category-${index}`"
            :value="category"
          >
            {{category}}
          </option>
        </select>
        <transition-group name="list-complete">
            <a 
                class="blog-list__card" 
                v-for="(post, index) in this.filteredItems" 
                :key="`key-${index}`" 
                :href="`/blog/${post.categories[0].name}/${post.slug}`"
            >
                <img :src="post.featured_image" />
                <h1>{{post.title}}</h1>
                <p>{{post.summary}}</p>
            </a>
        </transition-group>
    </div>
</template>

<script>
import { butter } from '~/plugins/buttercms';

export default {
  data() {
    return {
      search: '',
      page_title: 'Blog',
      posts: [],
      categories: []
    }
  },
  computed: {
    filteredItems() {
      return this.posts.filter(post => {
         return post.categories[0].name.indexOf(this.search) > -1
      })
    }
  },
  async fetch() {
    butter.post
      .list({
        page: 1,
        page_size: 10
      })
      .then((res) => {
        const data = res.data.data
        this.posts = data;
        let categories = [];

        data.forEach((item) => {
          let category = item.categories[0].name;
          if (!this.categories.includes(category)) {
            this.categories.push(item.categories[0].name)
          }
        })
        console.log(this.categories)
      })
  }
}
</script>

<style lang="scss">
.blog-list {
    $root: &;
    padding: 2rem;

    > span {
        padding: 2rem;
        display: grid;
        grid-template-columns: repeat(3,minmax(200px,.33fr));
    }

    &__card {
        max-width: 300px;
        height: auto;
        margin: 0 auto;
        display: flex;
        justify-content: center;
        flex-direction: column;
        transition: all 1s;

        img {
            height: 200px;
            width: inherit;
            position: relative;
            object-fit: cover;
        }
    }
}

.list-complete-enter, .list-complete-leave-to {
  opacity: 0;
  transform: translateY(30px);
}

.list-complete-leave-active {
  position: absolute;
}
</style>