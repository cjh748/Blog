<template>
    <div>
        <carousel 
            class="carousel" 
            :per-page-custom="[[1140, 3],[800, 2], [0, 1]]"
            :autoplay=true
            :autoplay-hover-pause=true
            :scroll-per-page=true
            :loop=true
        >
            <slide 
                 class="carousel__card"
                v-for="(card, index) in cards" :key="`${card}${index}`"
                navigate-to="/google"
            >
                <a class="carousel__card-content" :href="`blog/${card.categories[0].slug}/${card.slug}`">
                <div>
                    <img class="carousel__card-content-image" :src="card.featured_image" />
                    <h3>{{card.title}}</h3>
                    <span>{{card.author.first_name}} {{ card.author.last_name }} &bull;</span>
                    <span><em>{{ formatDate(card.created) }}</em></span>
                    <p>{{card.meta_description}}</p>
                    <p>{{card.categories[0].slug}}</p>
                    </div>
                </a>
            </slide>
        </carousel>
    </div>
</template>

<script>
import Vue from 'vue';
import moment from 'moment';
import { butter } from '~/plugins/buttercms';
import { Carousel, Slide } from 'vue-carousel';

export default Vue.extend({
    name: 'blog-carousel',
    components: { Carousel, Slide },
    data() {
        return {
            cards: []
        }
    },
    methods: {
      formatDate(date) {
        return moment(String(date)).format('dddd, MMMM Do YYYY')
      }
    },
      async fetch() {
        butter.post.list({
            page: 1,
            page_size: 10
        }).then((res) => {
            this.cards = res.data.data
        })
  }
})
</script>

<style lang="scss">
.carousel {
    &__card {
        padding: 2rem 1rem;
        border-radius: 16px;

        &:hover {
            background: $color-light-grey;
        }

        &-content {
            &-image{
                max-width: 100%;
                border-radius: 16px;
            }
        }
    }
}
</style>