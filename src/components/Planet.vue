<script setup lang="ts">
import { onMounted } from 'vue'
import planetImg from '../assets/planet.webp'
import gsap from 'gsap'

onMounted(() => {
  gsap.fromTo(
    '#planet h2',
    { opacity: 0 },
    {
      opacity: 1,
      duration: 1.7,
      ease: 'cubic-bezier(.37,0,.63,1)',
      scrollTrigger: {
        trigger: '#planet h2',
        start: 'top 60%',
      },
    }
  )
  gsap.fromTo(
    '#planet p',
    { opacity: 0 },
    {
      opacity: 1,
      duration: 1.7,
      ease: 'cubic-bezier(.37,0,.63,1)',
      scrollTrigger: {
        trigger: '#planet p',
        start: 'top 60%',
      },
    }
  )
  gsap.fromTo(
    '#planet .img-container',
    { y: 450 },
    {
      y: 0,
      duration: 2,
      ease: 'cubic-bezier(.455, .03, .515, .955)',
      scrollTrigger: {
        trigger: '#planet p',
        start: 'top 55%',
      },
    }
  )
  gsap.fromTo(
    '#planet .img-container img',
    { scale: 0.3 },
    {
      scale: 1,
      duration: 2.5,
      delay: 0.5,
      ease: 'cubic-bezier(.455, .03, .515, .955)',
      scrollTrigger: {
        trigger: '#planet p',
        start: 'top 55%',
      },
    }
  )
})
</script>

<template>
  <section id="planet">
    <h2>
      Today, we have <span>the most extensive portfolio</span> and project scope
      in the premium segment
    </h2>
    <p>
      Over 600 projects in 32 countries, with an average area starting from 900
      m². More than two million people worldwide follow the development of
      Studia 54, including celebrities, renowned designers, and architects
    </p>
    <div class="img-container">
      <img :src="planetImg" alt="Planet Image" />
    </div>
  </section>
</template>

<style scoped>
#planet {
  padding-top: clamp(80px, 50.8738px + 7.767vw, 200px);
  position: relative;

  &::before {
    background: linear-gradient(
      transparent 0%,
      transparent 60%,
      rgba(31, 31, 31, 0.9) 90%,
      #1f1f1f 95%
    );
    content: '';
    position: absolute;
    bottom: 0;
    left: 0;
    right: 0;
    top: 0;
    pointer-events: none;
    z-index: 1;
  }

  h2 {
    font-size: clamp(16px, 8.7184px + 1.9417vw, 46px);
    font-weight: 200;
    text-align: center;
    max-width: 1200px;
    text-transform: uppercase;
    margin: 0 auto;

    span {
      color: #d38c37;
    }
  }

  p {
    font-size: clamp(12px, 10.0583px + 0.5178vw, 20px);
    font-weight: 200;
    max-width: 1000px;
    text-align: center;
    margin: 30px auto 0 auto;
  }

  .img-container {
    max-height: 900px;
    overflow: hidden;

    img {
      max-width: 100%;
      mask-image: linear-gradient(to top, transparent 0%, #1f1f1f 10%),
        linear-gradient(to bottom, transparent 0%, #1f1f1f 10%),
        linear-gradient(to left, transparent 0%, #1f1f1f 10%),
        linear-gradient(to right, transparent 0%, #1f1f1f 10%);
      mask-composite: intersect;
      -webkit-mask-image: linear-gradient(to top, transparent 0%, #1f1f1f 10%),
        linear-gradient(to bottom, transparent 0%, #1f1f1f 10%),
        linear-gradient(to left, transparent 0%, #1f1f1f 10%),
        linear-gradient(to right, transparent 0%, #1f1f1f 10%);
      -webkit-mask-composite: intersect;
    }
  }
}
</style>
