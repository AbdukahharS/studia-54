<script setup lang="ts">
import NavBar from './components/NavBar.vue'
import heroVideo from './assets/hero.mp4'
import poster from './assets/hero-poster.webp'
</script>

<template>
  <NavBar />
  <section id="hero">
    <video :poster="poster" :src="heroVideo" autoplay muted loop></video>
  </section>
</template>

<style scoped>
#hero {
  width: 100%;
  height: 100vh;
  overflow: hidden;
  
  video {
    width: 100%;
    height: 100%;
    object-fit: cover;
  }
}
</style>
