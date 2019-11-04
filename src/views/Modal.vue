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

    <vue-glide v-if="!isLoading" :perView="3">
      <vue-glide-slide v-for="image in images" :key="image">
        <img :src="image">
      </vue-glide-slide>
    </vue-glide>
  </div>
</template>

<script>
import { Glide, GlideSlide } from 'vue-glide-js'
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
      [GlideSlide.name]: GlideSlide
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
  img {
    width: 100%;
    height: 100%;
    max-height: 400px;
    object-fit: cover;
  }
</style>
