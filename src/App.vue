<template>
  <div id="app">
    <Home/>
  </div>
</template>

<script lang="ts">
// import Vue from 'vue';
import Home from './components/Home.vue';

export default {
  name: 'app',
  components: {
    Home,
  },
};
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 50px;
}
</style>
