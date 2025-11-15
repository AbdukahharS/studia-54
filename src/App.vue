<script setup lang="ts">
import { onMounted, ref } from 'vue'
import gsap from 'gsap'
// Components
import NavBar from './components/NavBar.vue'
import Planet from './components/Planet.vue'
import Architecture from './components/Architecture.vue'
// Assets
import heroVideo from './assets/hero.mp4'
import poster from './assets/hero-poster.webp'
import logo from './assets/logo-small.svg'
import chatIcon from './assets/chat-icon.svg'
import profileIcon from './assets/profile-icon.svg'
import closeIcon from './assets/close.svg'

const isChatOpen = ref(false)

onMounted(() => {
  const chatContainer = document.querySelector('.chat-container')
  
  // Initialize chat as closed
  gsap.set(chatContainer, {
    clipPath: 'inset(100% 0% 0% 100% round 40px)',
  })
})

const toggleChat = () => {
  const chatContainer = document.querySelector('.chat-container')
  const triggerButton = document.querySelector('button.trigger')

  if (isChatOpen.value) {
    gsap.to(chatContainer, {
      clipPath: 'inset(100% 0% 0% 100% round 40px)',
      duration: 0.5,
      ease: 'power2.out',
    })
  } else {
    gsap.to(chatContainer, {
      clipPath: 'inset(0% 0% 0% 0% round 40px)',
      duration: 0.5,
      ease: 'power2.out',
    })
  }

  isChatOpen.value = !isChatOpen.value
  if (triggerButton) {
    triggerButton.classList.toggle('open')
  }
}
</script>

<template>
  <NavBar />
  <section id="hero">
    <video :poster="poster" :src="heroVideo" autoplay muted loop></video>
    <div class="intro">
      <img :src="logo" alt="Logo" />
      <h2>
        <span>A leading international bureau</span> for premium architectural
        and interior design
      </h2>
    </div>
  </section>
  <div id="chatAppWidget">
    <div class="chat-container">
      <div class="chat">
        <div class="header">
          <img :src="profileIcon" alt="Profile Icon" />
          <div>
            <span class="title">ChatApp</span>
            <span class="status">online</span>
          </div>
          <button @click="toggleChat"><img :src="closeIcon" alt="Close Icon" /></button>
        </div>
        <div class="content"></div>
      </div>
    </div>
    <button class="trigger" @click="toggleChat">
      <img :src="chatIcon" alt="Chat Icon" />
    </button>
  </div>
  <Planet />
  <Architecture />
</template>

<style scoped>
#hero {
  width: 100%;
  height: 100vh;
  overflow: hidden;
  position: relative;

  &::after {
    background: linear-gradient(180deg, #0000, #1d1d1df2 92.67%, #1f1f1f);
    content: '';
    position: absolute;
    bottom: 0;
    left: 0;
    width: 100%;
    height: 70%;
    pointer-events: none;
  }

  video {
    width: 100%;
    height: 100%;
    object-fit: cover;
  }

  .intro {
    position: absolute;
    bottom: 0;
    left: 0;
    z-index: 1; /* to appear above video and gradient */
    padding: 0 40px clamp(30px, -16.6667px + 6.0764cqi - 80px, 100px) 40px;

    img {
      height: 30px;
    }

    h2 {
      text-transform: uppercase;
      color: #fff;
      opacity: 0.75;
      font-size: clamp(14px, 10.1165px + 1.0356cqi, 30px);
      font-weight: 300;
      line-height: 1.25;
      max-width: clamp(400px, 288.3495px + 29.7735cqi, 837px);
      letter-spacing: 0.03em;

      span {
        color: #d38c37;
      }
    }
  }
}

#chatAppWidget {
  position: fixed;
  bottom: 10px;
  right: 10px;
  z-index: 1000;
  padding: 16px;

  button.trigger {
    background: #d38c37;
    border: none;
    border-radius: 50%;
    width: 49px;
    height: 49px;
    display: flex;
    align-items: center;
    justify-content: center;
    cursor: pointer;
    position: relative;
    display: inline-block;

    &:not(.open)::before {
      content: '';
      position: absolute;
      inset: 0;
      border-radius: 50%;
      background: #d38c37;
      animation: ping 2s cubic-bezier(0, 0, 0.2, 1) infinite;
    }

    img {
      width: 40px;
      height: 40px;
      position: relative;
      z-index: 1;
    }
  }

  .chat-container {
    padding: 20px;
    display: inline-block;

    .chat {
      width: 375px;
      height: 657px;
      background: #fff;
      border-radius: 20px;
      overflow: hidden;

      .header {
        display: flex;
        flex-direction: row;
        gap: 10px;
        background: linear-gradient(
          135deg,
          rgb(255, 215, 215),
          rgb(255, 241, 193)
        );
        padding: 25px 25px 20px 36px;

        img {
          width: 48px;
          height: 48px;
        }

        div {
          flex: 1;
          color: #252b36;
          font-size: 14px;
          display: flex;
          flex-direction: column;
          justify-content: center;

          .title {
            display: block;
            font-weight: 700;
            line-height: 17px;
          }
        }

        button {
          background: none;
          border: none;
          padding: 0;
          cursor: pointer;
          height: fit-content;
          padding: 8px;

          img {
            width: 16px;
            height: 16px;
          }
        }
      }
    }
  }
}

@keyframes ping {
  75%,
  100% {
    transform: scale(1.75);
    opacity: 0;
  }
}
</style>
