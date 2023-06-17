<script setup>
import {RouterView } from 'vue-router'
import Header from './components/Header.vue';
</script>

<template>
  <Header />
  <RouterView />
</template>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Comic+Neue:ital,wght@0,300;0,400;0,700;1,300&display=swap');

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
.container {
  max-width: 1200px;
  margin: 0 auto;
}
body {
  font-family: 'Comic Neue', cursive;
}
</style>
