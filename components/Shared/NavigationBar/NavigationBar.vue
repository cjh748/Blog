<template>
  <div>
    <div class="navbar">
      <NuxtLink to="/">Home</NuxtLink>
      <NuxtLink to="/blog">Blogs</NuxtLink>
      <NuxtLink to="/about">About me</NuxtLink>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.component('navigation-bar', Vue.extend({
    name: 'NavigationBar'
}));
</script>

<style lang="scss">
.navbar {
    $root: &;

    background: white;
    height: auto;
    width: fit-content;
    display: flex;
    float: right;
    border-radius: 0 0 0 16px;

    a {
      padding: 1rem;
    }
}
</style>