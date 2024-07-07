<script setup>
import gsap from 'gsap';
import { onMounted, ref } from 'vue';
import { ScrollTrigger } from 'gsap/ScrollTrigger';
gsap.registerPlugin(ScrollTrigger);
const rankListContainer = ref(null);
const rankTitle = ref(null);

onMounted(() => {
  function getAmountWidth(el) {
    let w = el.scrollWidth;
    return w - window.innerWidth;
  }

  gsap.defaults({ ease: 'none' });
  gsap.to('.scroll span', {
    y: 20,
    yoyo: true,
    repeat: -1,
  });

  const tl = gsap.timeline({
    scrollTrigger: {
      trigger: rankListContainer.value,
      start: 'top top',
      end: '+=' + getAmountWidth(rankListContainer.value),
      pin: true,
      scrub: 1,
    },
  });
  tl.to(rankListContainer.value, {
    x: getAmountWidth(rankListContainer.value) * -1,
  });

  const tl3 = gsap.timeline({
    scrollTrigger: {
      trigger: rankTitle.value,
      start: 'left left',
      end: '+=' + getAmountWidth(rankTitle.value),
      pin: true,
      scrub: true,
      horizontal: true,
      containerAnimation: tl,
      markers: true,
    },
  });

  tl3.to('h2', {
    x: getAmountWidth(rankTitle.value),
  });
});
</script>
<template>
  <div ref="rankListContainer" class="rankListContainer">
    <div class="scroll">
      <span>👇 Scroll</span>
    </div>
    <div ref="rankTitle" class="rankTitle">
      <h2>Horizontal Scrolling</h2>
      <div class="cardList">
        <div v-for="n in 5" class="card">
          <h1>title</h1>
          <p>content</p>
        </div>
      </div>
    </div>
  </div>
</template>
<style scoped>
.rankListContainer {
  display: flex;
  height: 100vh;
  width: fit-content;
  gap: 20px;
}
.scroll {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100vw;
  font-size: 64px;
}
.rankTitle {
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  padding: 62px;
}
h2 {
  width: fit-content;
}
.cardList {
  display: flex;
  gap: 40px;
  padding-right: 30vw;
}
.card {
  background-color: orange;
  width: 300px;
  height: 350px;
}
</style>
