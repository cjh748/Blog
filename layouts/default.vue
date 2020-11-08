<template>
  <div>
      <div class="main">
        <Introduction />
        <div class="main-portfolio">
          <navigation-bar></navigation-bar>
          <Nuxt />
        </div>  
      </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue';
import Introduction from '../components/Shared/Introduction/Introduction.vue';

export default Vue.extend({
  components: {
    Introduction
  }
})
</script>


<style lang="scss">
html {
  font-family:
    'Source Sans Pro',
    -apple-system,
    BlinkMacSystemFont,
    'Segoe UI',
    Roboto,
    'Helvetica Neue',
    Arial,
    sans-serif;
  font-size: 16px;
  word-spacing: 1px;
  -ms-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased;
  box-sizing: border-box;
}

*,
*::before,
*::after {
  box-sizing: border-box;
  margin: 0;
}

.button--green {
  display: inline-block;
  border-radius: 4px;
  border: 1px solid #3b8070;
  color: #3b8070;
  text-decoration: none;
  padding: 10px 30px;
}

.button--green:hover {
  color: #fff;
  background-color: #3b8070;
}

.button--grey {
  display: inline-block;
  border-radius: 4px;
  border: 1px solid #35495e;
  color: #35495e;
  text-decoration: none;
  padding: 10px 30px;
  margin-left: 15px;
}

.button--grey:hover {
  color: #fff;
  background-color: #35495e;
}

.main {
  $root: &;
  display: flex;
  flex-direction: row;
  width: 100%;
  height: 100%;

  &-portfolio {
    display: flex;
    flex-direction: column;
    width: calc(100% - 242px);
  }
}
</style>
