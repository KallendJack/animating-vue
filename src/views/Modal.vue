<template>
  <div>
    <h1>This is the modal page</h1>

    <button @click="toggleModal">Open</button>

    <transition name="fade">
      <div v-if="isOpen" class="modal">
        <p>
          <button @click="toggleModal">Close</button>
        </p>
      </div>
    </transition>

    <!-- <vue-glide v-if="!isLoading" :perView="3">
      <template slot="control">
        <button data-glide-dir="<">Start</button>
        <button data-glide-dir=">">End</button>
      </template>
      <vue-glide-slide v-for="image in images" :key="image">
        <img :src="image" />
      </vue-glide-slide>
    </vue-glide> -->

    <!-- <carousel-3d v-if="!isLoading" :controls-visible="true" :clickable="false" :disable3d="true">
    <slide :index="1">
      <img :src="images[0]" />
    </slide>
    <slide :index="2">
      <img :src="images[1]" />
    </slide>
    <slide :index="3">
      <img :src="images[2]" />
    </slide>
    <slide :index="4">
      <img :src="images[3]" />
    </slide>
    <slide :index="5">
      <img :src="images[4]" />
    </slide>
    <slide :index="6">
      <img :src="images[5]" />
    </slide>
  </carousel-3d> -->
<vueper-slides ref="myVueperSlides" class="no-shadow" :visible-slides="2.5" :slide-ratio="1/4" :dragging-distance="70">
  <vueper-slide v-for="(image, i) in images" :key="i" :image="image"></vueper-slide>
</vueper-slides>

<button @click="$refs.myVueperSlides.previous()">Previous</button>
<button @click="$refs.myVueperSlides.next()">Next</button>

  </div>
</template>

<script>
import { Glide, GlideSlide } from 'vue-glide-js'
import { Carousel3d, Slide } from 'vue-carousel-3d';
import { VueperSlides, VueperSlide } from 'vueperslides'
import 'vueperslides/dist/vueperslides.css'
import axios from 'axios'
export default {
  mounted() {
    axios
      .get(
        'https://api.unsplash.com/photos/?client_id=365810b92388cb95de07bbdad14e6e3a3515a8ce0853219faed2acccd301f609'
      )
      .then(response => {
        response.data.forEach(image => {
          this.images.push(image.urls.regular)
          this.isLoading = false
        })
      })
  },
  components: {
    [Glide.name]: Glide,
    [GlideSlide.name]: GlideSlide,
    Carousel3d,
    Slide,
    VueperSlides, VueperSlide
  },
  data() {
    return {
      isOpen: false,
      images: [],
      isLoading: true
    }
  },
  methods: {
    toggleModal() {
      this.isOpen = !this.isOpen
    }
  }
}
</script>

<style lang="scss" scoped>
div[data-glide-el='controls'] {
  width: 100px;
  height: 100px;
  background-color: red;
}

img {
  width: 100%;
  height: 100%;
  max-height: 400px;
  object-fit: cover;
}

.carousel-3d-controls {
  top: 0;
  position: fixed !important;
  background-color: red;
}
</style>
