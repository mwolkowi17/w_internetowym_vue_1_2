<script setup>
import HelloWorld from './components/HelloWorld.vue'

import MainComp from './components/MainComp.vue'
import { ref, onMounted, onUnmounted } from 'vue'

const scale = ref(1)

function updateScale() {
  const widthRatio = window.innerWidth / 1920//2560//1920
  const heightRatio = window.innerHeight / 1080//1440//1080
  scale.value = Math.min(widthRatio, heightRatio)
}

onMounted(() => {
  updateScale()
  window.addEventListener('resize', updateScale)
})

onUnmounted(() => {
  window.removeEventListener('resize', updateScale)
})
</script>

<template>
   <div class="game-container">
   <MainComp  />
   </div>
</template>

<style scoped>
.game-container {
  width: 100vw;
  height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: flex-start;

  max-width: 1920px;
  max-height: 1080px;

  aspect-ratio: 16 / 9;

  margin: auto;

  background-size: cover;
  background-position: center;
}
</style>
