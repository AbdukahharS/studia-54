<script setup lang="ts">
import { onMounted, ref } from 'vue'
import gsap from 'gsap'
import ScrollTrigger from 'gsap/ScrollTrigger'
import videoSrc from '../assets/hero.mp4'
import poster from '../assets/hero-poster.webp'

interface Dropdown {
  title: string
  content: string[]
}

const activeDropdown = ref(0)

const dropdowns: Dropdown[] = [
  {
    title: 'A home that surrounds you with warmth and care',
    content: [
      'In creating a home, we strive to <span>fully understand your vision</span> — what details inspire you and how you imagine the perfect retreat',
      'We design homes in Studia 54’s signature style, using our own architectural and structural solutions, incorporating <span>natural materials</span>, and selecting a color palette that harmonizes with the surroundings.',
      'This approach allows the home to blend seamlessly with the landscape, creating a sense of complete unity with nature.',
    ],
  },
  {
    title: 'Bringing complex projects to life',
    content: [
      '<span>Over 10 years</span> of experience handling complex architectural, structural, and engineering challenges have made us international experts in <span>executing large-scale premium projects</span>, including residences exceeding 10,000 m²',
      'With a comprehensive approach from our leading architects and engineers, we create personalized living scenarios, <span>shaping an environment that takes care of you</span>',
    ],
  },
  {
    title: 'Adapting to your lifestyle',
    content: [
      'A cozy family living room for relaxation, a grand reception hall for social events, a private spa with a beauty salon, a functional fitness and yoga space. Thoughtfully designed walking paths that match your pace, secluded relaxation areas by the fire, and spacious heated terraces with bioclimatic protection from the elements.',
      '<span>By immersing ourselves in your lifestyle, we offer our vision of your ideal home — crafted in harmony with nature, for you and your family</span>',
    ],
  },
]

const toggleDropdown = (index: number) => {
  activeDropdown.value = index
}

onMounted(() => {
  gsap.registerPlugin(ScrollTrigger)

  // Calculate scale based on viewport vs container dimensions
  const videoElement = document.querySelector('#architecture video')
  const archElement = document.querySelector('#architecture')
  const videoRect = videoElement?.getBoundingClientRect()
  const archRect = archElement?.getBoundingClientRect()

  if (videoRect) {
    // Calculate how much we need to scale the video to cover the viewport
    const deltaY = archRect ? videoRect.top - archRect.top : 0

    gsap.fromTo(
      '#architecture video',
      {
        width: window.innerWidth - 5,
        height: window.innerHeight,
        x: -videoRect.left,
        y: -deltaY,
        transformOrigin: 'top left',
      },
      {
        width: '100%',
        height: '100%',
        x: 0,
        y: 0,
        ease: 'none',
        scrollTrigger: {
          trigger: '#architecture',
          start: 'top top',
          end: 'bottom bottom',
          scrub: 0.5,
        },
      }
    )
  }

  ScrollTrigger.create({
    trigger: '#architecture',
    start: '200vh top',
    end: 'bottom bottom',
    onEnter: () => {
      // Animation when scrolling down past 200px
      gsap.to('#architecture .crumb h3', {
        x: 0,
        y: 0,
        scale: '1',
        color: '#d38c37',
        duration: 0.8,
        ease: 'power2.inOut',
      })
    },
    onLeaveBack: () => {
      // Reverse animation when scrolling back up above 200px
      gsap.to('#architecture .crumb h3', {
        x: '10vw',
        y: '10vw',
        scale: 1.5,
        color: '#fff',
        duration: 0.8,
        ease: 'power2.inOut',
      })
    },
  })
})
</script>

<template>
  <section id="architecture">
    <div class="sticky-container">
      <div class="crumb">
        <span>.</span>
        <h3 class="title">/ Architectural design</h3>
      </div>
      <div class="content">
        <div class="dropdown-container">
          <div
            v-for="(dropdown, index) in dropdowns"
            :key="index"
            class="dropdown"
            :class="{ 'dropdown-active': activeDropdown === index }"
          >
            <button class="title" @click="toggleDropdown(index)">
              <h3>{{ dropdown.title }}</h3>
              <span class="arrow-container">
                <svg
                  class="arrow"
                  width="30"
                  height="25"
                  viewBox="0 0 30 25"
                  fill="none"
                  xmlns="http://www.w3.org/2000/svg"
                >
                  <path
                    d="M17.8627 24.1455L29.5039 12.5591L17.8627 0.972761C17.7576 0.836059 17.624 0.723319 17.471 0.642175C17.3181 0.56103 17.1493 0.513374 16.9761 0.502433C16.8029 0.491493 16.6294 0.517523 16.4672 0.578762C16.3051 0.64 16.1581 0.735017 16.0363 0.85738C15.9145 0.979743 15.8206 1.1266 15.7611 1.288C15.7016 1.4494 15.6778 1.62158 15.6913 1.79288C15.7048 1.96418 15.7554 2.13061 15.8395 2.28089C15.9236 2.43117 16.0394 2.5618 16.1789 2.66394L24.8886 11.3597L1.71527 11.3597C1.39399 11.3597 1.08588 11.4861 0.858707 11.711C0.631533 11.9359 0.503906 12.241 0.503906 12.5591C0.503906 12.8772 0.631532 13.1823 0.858707 13.4072C1.08588 13.6322 1.39399 13.7585 1.71527 13.7585L24.8886 13.7585L16.1789 22.4543C15.9524 22.6802 15.8258 22.9859 15.827 23.3041C15.8281 23.6224 15.9569 23.9272 16.185 24.1515C16.4131 24.3758 16.7218 24.5011 17.0433 24.5C17.3647 24.4989 17.6726 24.3714 17.8991 24.1455L17.8627 24.1455Z"
                  />
                </svg>
              </span>
            </button>
            <div class="dropdown-content">
              <div class="inner-container">
                <div class="content-text">
                  <p
                    v-for="(item, itemIndex) in dropdown.content"
                    :key="itemIndex"
                    v-html="item"
                  ></p>
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="video-container">
          <video :src="videoSrc" :poster="poster" muted autoplay loop></video>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
#architecture {
  height: 250vh;
  margin-top: clamp(50px, 13.5922px + 9.7087vw, 200px);
  position: relative;

  .sticky-container {
    position: sticky;
    top: 0;
    padding: 0 40px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    height: 100dvh;

    .crumb {
      position: relative;
      margin-bottom: clamp(30px, 22.7184px + 1.9417cqi, 60px);

      span {
        color: transparent;
      }

      h3 {
        position: absolute;
        z-index: 2;
        font-size: clamp(14px, 10.1165px + 1.0356cqi, 30px);
        transform: translate(10vw, 10dvw) scale(1.5);
        text-transform: uppercase;
        color: #fff;
        left: 0;
        top: 0;
        margin: 0;
        font-weight: 300;
      }
    }

    .content {
      display: grid;
      grid-template-columns: 37% calc(63% - 20px);
      grid-template-rows: clamp(450px, 283.3333px + 21.7014cqi, 700px);
      gap: 20px;

      .dropdown-container {
        display: flex;
        flex-direction: column;
        gap: clamp(10px, 0.5vw, 15px);
        overflow: visible;

        .dropdown {
          display: flex;
          flex-direction: column;
          position: relative;
          background: #252525;
          border-radius: clamp(15px, 8.932px + 1.6181cqi, 40px);
          backdrop-filter: blur(10px);
          transition: flex-grow 1.2s ease, flex-shrink 1.2s ease,
            flex-basis 1.2s ease;
          flex: 0 0 auto;
          overflow: hidden;

          &:not(.dropdown-active) {
            flex: 0 0 auto;

            .arrow {
              transform: rotate(45deg);
              fill: #fff9;
            }

            .dropdown-content {
              max-height: 0;
              opacity: 0;
              visibility: hidden;
              pointer-events: none;
            }
          }

          &.dropdown-active {
            flex: 1 1 0;

            .arrow {
              transform: rotate(-45deg);
              fill: #d38c37;
            }

            .dropdown-content {
              max-height: 1000px;
              opacity: 1;
              visibility: visible;
              pointer-events: auto;
            }
          }

          .title {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: clamp(15px, 1.5vw, 25px) clamp(20px, 2vw, 30px);
            background: transparent;
            border: none;
            cursor: pointer;
            color: #fff;
            text-align: left;
            width: 100%;

            h3 {
              text-transform: uppercase;
              font-size: clamp(14px, 11.5728px + 0.6472cqi, 24px);
              font-weight: 300;
              margin: 0;
              line-height: 1.35;
            }

            .arrow-container {
              flex-shrink: 0;
              margin-left: 20px;

              .arrow {
                width: 24px;
                height: 29px;
                transition: all 0.6s ease;
              }
            }

            &:hover {
              .arrow {
                fill: #d38c37;
              }
            }
          }

          .dropdown-content {
            overflow: hidden;
            transition: max-height 0.7s, opacity 0.5s, visibility 0.5s;

            .inner-container {
              padding: 0 clamp(20px, 2vw, 30px) clamp(20px, 2vw, 30px);

              .content-text {
                p {
                  font-size: clamp(14px, 12.5437px + .3883cqi, 20px);
                  line-height: 1.2;
                  color: #979797;
                  margin: 0 0 0.6em 0;
                  letter-spacing: 0.025rem;

                  &:deep(span) {
                    color: #d38c37;
                  }

                  &:last-child {
                    margin-bottom: 0;
                  }
                }
              }
            }
          }
        }
      }

      .video-container {
        position: relative;

        video {
          position: absolute;
          object-fit: cover;
          border-radius: clamp(15px, 1.6181cqi + 8.932px, 40px);
        }
      }
    }
  }
}
</style>
