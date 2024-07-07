<script setup>
const props = defineProps(['r']);
</script>
<template>
  <div class="graph" :style="{ width: r.value + 'px' }"></div>
</template>
<style scoped>
.graph {
  height: 20px;
  background-color: dodgerblue;
}
</style>
