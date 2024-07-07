<script setup>
import gsap from 'gsap';
import { computed, onMounted, ref } from 'vue';
import { ScrollTrigger } from 'gsap/ScrollTrigger';
gsap.registerPlugin(ScrollTrigger);

const props = defineProps(['r']);
const width = 300; // Adjust as per your design requirements
const height = 300; // Adjust as per your design requirements

const r = ref({
  value1: 0,
  value2: 0,
  value3: 0,
});

onMounted(() => {
  const tl = gsap.timeline({
    scrollTrigger: {
      trigger: '.graph',
      start: 'top center',
    },
  });
  tl.to(r.value, {
    value1: 5,
    duration: 0.3,
    ease: 'none',
  })
    .to(r.value, {
      value2: 1,
      duration: 0.3,
      ease: 'none',
    })
    .to(r.value, {
      value3: 3,
      duration: 0.3,
      ease: 'none',
    });
});

// Function to calculate radius based on rating and segment index
const calculateRadius = rating => {
  const maxRating = 5; // Example: maximum rating value
  const minRadius = 20; // Example: minimum radius value
  const maxRadius = 150; // Example: maximum radius value

  // Calculate radius based on rating
  const normalizedRating = Math.min(Math.max(rating, 0), maxRating); // Ensure rating is within bounds
  const radiusRange = maxRadius - minRadius;
  const radius = minRadius + (normalizedRating / maxRating) * radiusRange;

  return radius;
};

// Computed property to generate dynamic path based on rating and segment index
const fanPath = (r, index) =>
  computed(() => {
    const radius = calculateRadius(r);
    // const radius = calculateRadius(props.ratings[index]);

    const centerX = width / 2; // Center X of the SVG
    const centerY = height / 2; // Center Y of the SVG

    // Calculate the base start and end angles for each segment (without rotation)
    const baseStartAngle = (index * 120 - 60) * (Math.PI / 180);
    const baseEndAngle = ((index + 1) * 120 - 60) * (Math.PI / 180);

    // Adjust angles by rotation angle
    const rotatedStartAngle = baseStartAngle + -90 * (Math.PI / 180);
    const rotatedEndAngle = baseEndAngle + -90 * (Math.PI / 180);

    //   const startAngle = (index * 120 - 60) * (Math.PI / 180); // Start angle of the fan segment
    //   const endAngle = ((index + 1) * 120 - 60) * (Math.PI / 180); // End angle of the fan segment

    // Calculate points for the fan shape
    const x1 = centerX + radius * Math.cos(rotatedStartAngle);
    const y1 = centerY + radius * Math.sin(rotatedStartAngle);
    const x2 = centerX + radius * Math.cos(rotatedEndAngle);
    const y2 = centerY + radius * Math.sin(rotatedEndAngle);

    // Generate the fan shape path data
    return `M${centerX} ${centerY} L${x1} ${y1} A${radius} ${radius} 0 0 1 ${x2} ${y2} Z`;
  });
</script>

<template>
  <div class="denkyuu">
    <svg
      class="graph"
      viewBox="0 0 300 300"
      fill="none"
      xmlns="http://www.w3.org/2000/svg"
    >
      <path v-if="r" :d="fanPath(r.value1, 0).value" fill="#FFE24D" />
      <path v-if="r" :d="fanPath(r.value2, 1).value" fill="#FFED90" />
      <path v-if="r" :d="fanPath(r.value3, 2).value" fill="#FBD300" />
    </svg>
    <img
      src="https://icon-pit.com/wp-content/uploads/2020/01/denkyuu_light-bulb_lighting_5198.png"
      alt=""
    />
  </div>
  <div class="">3.5</div>
</template>

<style scoped>
.denkyuu {
  position: relative;
  width: 600px;
  height: 600px;
}
.graph {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 30%;
  height: 30%;
}

img {
  position: absolute;
  width: 100%;
  height: 100%;
}
</style>
