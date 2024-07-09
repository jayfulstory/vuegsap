<script setup>
import { RouterLink, RouterView } from 'vue-router';
import HorizontalView from './views/HorizontalView.vue';
</script>

<template>
  <div class="nav">
    <RouterLink to="/">
      <span> Home </span>
    </RouterLink>
  </div>
  <RouterView />
  <HorizontalView />
</template>

<style scoped>
.nav {
  position: fixed;
  display: flex;
  align-items: center;
  background-color: dodgerblue;
  width: 100vw;
  height: 48px;
  z-index: 10;
}
.nav span {
  padding-left: 32px;
}
</style>
