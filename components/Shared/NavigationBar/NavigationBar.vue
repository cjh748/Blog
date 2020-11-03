<template>
  <div>
    <b-navbar toggleable="lg" type="dark">
      <b-navbar-brand href="#">Welcome to my blog!</b-navbar-brand>

      <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

      <b-collapse id="nav-collapse" is-nav>
        <b-navbar-nav class="ml-auto">
          <b-nav-item href="#">
            <router-link to="/">Home</router-link>
          </b-nav-item>
          <b-nav-item href="#">
            <router-link to="/about">About</router-link>
          </b-nav-item>
          <b-nav-item-dropdown text="Blogs" right>
            <b-dropdown-item href="#">Travel</b-dropdown-item>
            <b-dropdown-item href="#">Development</b-dropdown-item>
            <b-dropdown-item href="#">Animals</b-dropdown-item>
            <b-dropdown-item href="#">Work</b-dropdown-item>
          </b-nav-item-dropdown>
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>
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

    &-dark {
        background-color: $color-coal;
    }
}
</style>