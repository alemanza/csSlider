<template>
  <div class="wrapper">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'app',
  components: {
    HelloWorld
  }
}
</script>

<style lang="scss">
@import './assets/scss/reset';
@import './assets/scss/fonts';
@import './assets/scss/base';
.wrapper{
  font-family: 'Chivo', Helvetica, Arial, sans-serif;
}
</style>
