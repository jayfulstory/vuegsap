<script setup>
import TestItem from '../TestItem.vue';
import RatingGraph from '../RatingGraph.vue';
</script>
<template>
  <div class="test">
    <RatingGraph />
    <TestItem />
  </div>
</template>
<style scoped>
.test {
  min-height: 100vh;
}
</style>
