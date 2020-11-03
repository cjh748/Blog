<template>
    <div class="intro">
        <router-link to="/" class="intro__logo">
            <img src="../../../assets/images/logo.png" />
        </router-link>
        <div class="intro__detail">
          <p>Hi, I am</p>
          <h3>Chris Homer</h3>
          <img class="intro__detail-image" src="../../../assets/images/profile.jpg" />
          <p>I'm a software developer working at Valtech</p>
        </div>
        <SocialMediaIconGroup />
      </div>
</template>

<script lang="ts">
import Vue from 'vue';
import SocialMediaIconGroup from '../SocialMedia/SocialMediaIconGroup.vue';

export default Vue.extend({
    name: 'Introduction',
    components: {
        SocialMediaIconGroup
    }
})
</script>

<style lang="scss">
.intro {
    display: flex;
    justify-content: space-between;
    flex-direction: column;
    position: sticky;
    text-align: center;
    border-right: $color-coal 2px solid;
    max-width: $intro-width;
    color: $color-coal;
    padding: 2rem;
    min-width: 300px;
    height: 100vh;
    top: 0;

    &__logo {
        text-align: center;
        > img {
        width: 100%;
        margin: auto;
        }
    }

    &__detail {
        &-image{
        width: 150px;
        border-radius: 50em;
        }
    }
}
</style>