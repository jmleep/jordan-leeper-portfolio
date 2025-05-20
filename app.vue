<template>
  <div class="min-h-screen px-16 py-8 relative">
    
    <div class="absolute inset-0 bg-black">
      <div class="scene">
        <div class="cube-grid">
          <div v-for="i in 15" :key="i" class="cube" :ref="el => { if (el) cubes[i-1] = el }">
            <div class="cube__face cube__face--front"></div>
            <div class="cube__face cube__face--back"></div>
            <div class="cube__face cube__face--right"></div>
            <div class="cube__face cube__face--left"></div>
            <div class="cube__face cube__face--top"></div>
            <div class="cube__face cube__face--bottom"></div>
          </div>
        </div>
      </div>
    </div>
    <div class="relative z-10">
      <ContactLinks />
      <div class="my-16">
        <AboutMe />
      </div>
      <BlogPosts />
      <Projects />
    </div>
  </div>
</template>

<script setup lang="ts">
import AboutMe from '@/components/AboutMe.vue'
import Projects from '@/components/Projects.vue'
import BlogPosts from '@/components/BlogPosts.vue'
import ContactLinks from '@/components/ContactLinks.vue'

import { onMounted, ref } from 'vue'

const cubes = ref<(HTMLElement | null)[]>([])
let rotations = Array(15).fill(0)

onMounted(() => {
  // Set initial rotations
  cubes.value.forEach((cube, index) => {
    if (cube) {
      const initialRotation = index * 45; // 45 degrees between each cube
      cube.style.transform = `translateZ(-75px) rotateY(${initialRotation}deg) rotateX(${initialRotation * 0.5}deg)`;
    }
  });

  window.addEventListener('scroll', () => {
    cubes.value.forEach((cube, index) => {
      if (cube) {
        rotations[index] = window.scrollY * (0.3 + (index * 0.1))
        const initialRotation = index * 45;
        cube.style.transform = `translateZ(-75px) rotateY(${initialRotation + rotations[index]}deg) rotateX(${initialRotation * 0.5 + rotations[index] * 0.5}deg)`
      }
    })
  })
})
</script>

<style scoped>
html {
  scroll-behavior: smooth;
}

.scene {
  width: 1200px;
  height: 900px;
  position: fixed;
  top: 50%;
  left: 45%;
  transform: translate(-50%, -50%);
  perspective: 1500px;
  z-index: 0;
  margin: 0;
}

.cube-grid {
  position: absolute;
  width: 100%;
  height: 100%;
  top: 0;
  left: -100px;
  display: grid;
  grid-template-columns: repeat(5, 1fr);
  grid-template-rows: repeat(3, 1fr);
  gap: 100px 200px;
  padding: 100px 0;
  place-items: center;
}

.cube {
  width: 150px;
  height: 150px;
  position: relative;
  transform-style: preserve-3d;
  transform: translateZ(-75px);
  transition: transform 0.1s ease-out;
}

.cube__face {
  position: absolute;
  width: 150px;
  height: 150px;
  border: 2px solid white;
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(5px);
}

.cube__face--front  { transform: rotateY(  0deg) translateZ(75px); }
.cube__face--right  { transform: rotateY( 90deg) translateZ(75px); }
.cube__face--back   { transform: rotateY(180deg) translateZ(75px); }
.cube__face--left   { transform: rotateY(-90deg) translateZ(75px); }
.cube__face--top    { transform: rotateX( 90deg) translateZ(75px); }
.cube__face--bottom { transform: rotateX(-90deg) translateZ(75px); }
</style>