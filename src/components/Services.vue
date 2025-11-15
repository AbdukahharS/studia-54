<script setup lang="ts">
import Architecture from './Service.vue'
import heroVideo from '../assets/hero.mp4'
import heroPoster from '../assets/hero-poster.webp'
import interiorVideo from '../assets/interior.mp4'
import interiorPoster from '../assets/interior.webp'
import furnitureVideo from '../assets/furniture.mp4'
import furniturePoster from '../assets/furniture.webp'

interface Dropdown {
  title: string
  content: string[]
}

const architecturalDesignDropdowns: Dropdown[] = [
  {
    title: 'A home that surrounds you with warmth and care',
    content: [
      'In creating a home, we strive to <span>fully understand your vision</span> — what details inspire you and how you imagine the perfect retreat',
      "We design homes in Studia 54's signature style, using our own architectural and structural solutions, incorporating <span>natural materials</span>, and selecting a color palette that harmonizes with the surroundings.",
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

const interiorDesignDropdowns: Dropdown[] = [
  {
    title: 'Harmonizing space with flawless details',
    content: [
      'Our journey to creating your interior begins with an <span>in-depth understanding of your lifestyle and aspirations</span>, capturing the essence of your ideal home atmosphere.',
      'Our portfolio reflects Studia 54’s signature style — carefully curated color combinations and compositional accents that enhance spatial geometry, transforming interiors into a source of inspiration',
    ],
  },
  {
    title: 'Implementing design projects of all complexities',
    content: [
      'Thoughtful details add warmth, while lighting installations designed by our team and artworks by world-renowned artists infuse the space with depth and refined luxury.',
      '<span>For over 10 years</span>, we have been delivering complex high-end design projects, continuously refining our expertise — whether it’s a 1,000 m² luxury family apartment in Moscow, an intimate restaurant at Burj Khalifa, or a 6,800 m² palace in Saudi Arabia with exquisite Eastern influences',
    ],
  },
  {
    title: 'A multifaceted approach to interior creation',
    content: [
      'We see interiors as an inseparable extension of architecture. Just as an architect envisions the flow of life within a home, an interior designer completes this vision, meticulously shaping every detail to <span>create an atmosphere of harmony and absolute comfort</span',
    ],
  },
]

const furnitureDropdowns: Dropdown[] = [
  {
    title: 'Own production facility',
    content: [
      'Every detail of your project is executed with precision — exactly as envisioned during development. <span>From layout to exclusive furniture, everything is realized with meticulous accuracy.</span>',
      'Our <span>in-house 1,500 m² production facility</span> allows us to manufacture custom suede and veneer panels, complex cabinetry, and premium furniture collections',
    ],
  },
  {
    title: 'Unique products from our brand',
    content: [
      '<a href="https://fiftyfourms.com/en" _target="blank"><span>FiftyFourms</span></a> embodies our expertise in working with intricate materials and forms.',
      'Under the guidance of our Italian technologist, the combination of artisanal craftsmanship and state-of-the-art equipment results in <span>high-quality</span> pieces, distinguished by Studia 54’s signature design',
    ],
  },
]
</script>

<template>
  <div class="sections">
    <Architecture
      section-id="architectural-design"
      title="/ Architectural design"
      :dropdowns="architecturalDesignDropdowns"
      :video-src="heroVideo"
      :poster="heroPoster"
    />
    <Architecture
      section-id="interior-design"
      title="/ Interior design"
      :dropdowns="interiorDesignDropdowns"
      :video-src="interiorVideo"
      :poster="interiorPoster"
    />
    <Architecture
      section-id="furniture-production"
      title="/ Furniture production"
      :dropdowns="furnitureDropdowns"
      :video-src="furnitureVideo"
      :poster="furniturePoster"
    />
  </div>
</template>

<style scoped>
.sections {
  width: 100%;
}
</style>
