<template>
  <img class="logo" alt="Vue logo" src="./assets/images/logo/logo.png">
  <ContentBlock msg="File uploader" />
</template>

<script>
import ContentBlock from './components/ContentBlock.vue';

export default {
  name: 'App',
  components: {
    ContentBlock,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #fff;
  margin-top: 60px;
}
</style>
