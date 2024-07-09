<script setup>
import gsap from 'gsap';
import { onMounted, ref } from 'vue';

const circle = ref(null);

onMounted(() => {
  const length = Math.ceil(circle.value.getTotalLength());
  console.log(length);
  gsap.defaults({
    ease: 'none',
  });
  gsap.set(circle.value, {
    strokeDashoffset: length,
    strokeDasharray: length,
  });

  gsap.to(circle.value, {
    strokeDashoffset: 0,
    duration: 1.5,
  });

  const tl = gsap.timeline();

  tl.to('.rating', {
    opacity: 1,
    stagger: 0.5,
    duration: 0.3,
  })
    .to('.rating--1', {
      y: -5,
      yoyo: true,
      repeat: -1,
      duration: 1,
    })
    .to(
      '.rating--2',
      {
        y: -5,
        yoyo: true,
        repeat: -1,
        duration: 0.9,
      },
      '<+=0.5'
    )
    .to(
      '.rating--3',
      {
        y: -5,
        yoyo: true,
        repeat: -1,
        duration: 1.1,
      },
      '<-=0.5'
    );
});
</script>
<template>
  <div style="height: 100px; width: 200px"></div>
  <div class="graph">
    <svg
      width="100%"
      height="100%"
      viewBox="0 0 100 100"
      xmlns="http://www.w3.org/2000/svg"
    >
      <defs>
        <linearGradient
          id="blueYellowGradient"
          x1="0%"
          y1="0%"
          x2="100%"
          y2="100%"
        >
          <stop offset="0%" style="stop-color: orange; stop-opacity: 1" />
          <stop offset="100%" style="stop-color: yellow; stop-opacity: 1" />
        </linearGradient>
      </defs>
      <circle
        ref="circle"
        cx="50"
        cy="50"
        r="45"
        stroke="url(#blueYellowGradient)"
        stroke-width="10"
        style="transform: rotate(-90deg); transform-origin: center"
        fill="none"
      ></circle>
    </svg>
    <div class="rating rating--1">
      assdfsd<br /><small>asdasdfvd</small><br />3.5
    </div>
    <div class="rating rating--2">
      assdfsd<br /><small>asdasdfvd</small><br />4
    </div>
    <div class="rating rating--3">
      assdfsd<br />
      <small>asdasdfvd</small>
      <br />5
    </div>
  </div>
</template>
<style scoped>
.graph {
  position: relative;
  width: 400px;
  height: 400px;
}
svg {
  width: 200px;
  height: 200px;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
.rating {
  position: absolute;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  width: 100px;
  height: 100px;
  border-radius: 50%;
  text-align: center;
  background-color: rgba(250, 250, 252, 0.5);
  backdrop-filter: blur(4px);
  opacity: 0;
}
small {
  font-size: 10px;
}

.rating--1 {
  top: 30px;
  left: 130px;
}
.rating--2 {
  top: 200px;
  left: 250px;
}
.rating--3 {
  top: 200px;
  left: 40px;
}
</style>
