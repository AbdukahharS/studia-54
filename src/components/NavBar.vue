<script setup lang="ts">
import { onMounted } from 'vue'
import gsap from 'gsap'
import ScrollTrigger from 'gsap/ScrollTrigger'
import logo from '../assets/logo.svg'

gsap.registerPlugin(ScrollTrigger)

onMounted(() => {
  const links = document.querySelectorAll('.links a')
  const nav = document.querySelector('nav')

  // Underline hover animations
  links.forEach((link) => {
    const underline = link.querySelector('.underline')

    link.addEventListener('mouseenter', () => {
      gsap.to(underline, {
        scaleX: 1,
        duration: 0.3,
        transformOrigin: 'left',
        ease: 'power2.out',
      })
    })

    link.addEventListener('mouseleave', () => {
      gsap.to(underline, {
        scaleX: 0,
        duration: 0.3,
        transformOrigin: 'right',
        ease: 'power2.in',
      })
    })
  })

  // Scroll animation triggered at 200px
  ScrollTrigger.create({
    trigger: document.body,
    start: '100px top',
    end: '100px top',
    onEnter: () => {
      // Animation when scrolling down past 200px
      gsap.to(nav, {
        y: '-100%',
        opacity: 0,
        duration: 0.4,
        ease: 'power2.out',
      })
    },
    onLeaveBack: () => {
      // Reverse animation when scrolling back up above 200px
      gsap.to(nav, {
        y: 0,
        opacity: 1,
        duration: 0.4,
        ease: 'power2.out',
      })
    },
  })
})
</script>

<template>
  <nav>
    <img :src="logo" alt="Logo" />
    <div class="links">
      <a href="/about">
        ABOUT
        <span class="underline"></span>
      </a>
      <a href="/portfolio">
        PORTFOLIO
        <span class="underline"></span>
      </a>
      <a href="/contacts">
        CONTACTS
        <span class="underline"></span>
      </a>
      <a href="/services">
        SERVICES
        <span class="underline"></span>
      </a>
    </div>
    <button class="contact">CONTACT US</button>
    <div class="locales">
      <button>RU</button>
      <button class="current">EN</button>
    </div>
  </nav>
</template>

<style scoped>
nav {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  max-width: 100vw;
  z-index: 1000;
  background: linear-gradient(180deg, #1f1f1f66 -36.21%, #1f1f1f00);
  backdrop-filter: blur(6px);
  -webkit-backdrop-filter: blur(6px);
  padding: 25px clamp(20px, -48.9231px + 6.7308vw, 48px);
  display: flex;
  flex-direction: row;
  align-items: center;
  box-sizing: border-box;

  img {
    height: clamp(42px, 30px + 0.8333vw, 46px);
  }

  .links {
    display: flex;
    flex-direction: row;
    gap: 15px;
    flex: 1;
    justify-content: flex-end;

    a {
      font-size: 13px;
      letter-spacing: 0.09em;
      line-height: 16.35px;
      padding: 11px 16px;
      position: relative;
      display: inline-block;

      .underline {
        position: absolute;
        bottom: 8px;
        left: 16px;
        right: 16px;
        height: 1px;
        background-color: currentColor;
        transform: scaleX(0);
        transform-origin: left;
      }
    }
  }

  button.contact {
    border: none;
    background-color: #d38c37;
    color: #ffffff;
    padding: 12px;
    border-radius: 26px;
    width: 200px;
    font-size: 13px;
    letter-spacing: 0.09em;
    margin: 0 30px 0 15px;
    transition: background-color 0.3s ease-in-out;

    &:hover {
      background-color: #bf7a2b;
    }
  }

  .locales {
    display: flex;
    flex-direction: row;
    gap: 24px;
    align-items: center;

    &::before {
      height: 16px;
      width: 1px;
      background-color: #ffffff;
      content: '';
      display: inline-block;
    }

    button {
      border: none;
      background: none;
      color: #ffffff;
      letter-spacing: 0.09em;
      padding: 0;
      cursor: pointer;

      &.current {
        font-weight: 600;
      }
    }
  }
}
</style>
