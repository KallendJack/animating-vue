<template>
  <div v-if="!isLoading" class="list-container">
    <input type="text" v-model="newContact" placeholder="Name" />
    <button @click="addContact">Add Contact</button>
    <button @click="sortContacts">Sort</button>

    <transition-group name="slide-up" tag="ul" appear>
      <li v-for="contact in contacts" :key="contact">{{ contact }}</li>
    </transition-group>

    <input type="text" v-model="newImage" placeholder="Name" />
    <button @click="addImage">Add Image</button>
    <button @click="sortImages">Sort</button>
    <transition-group name="slide-up" appear class="gallery">
      <div v-for="image in images" :key="image" class="img-container">
        <img :src="image" />
      </div>
    </transition-group>
  </div>
</template>

<script>
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
  data() {
    return {
      newContact: '',
      contacts: ['Beau Thabeast', 'Cindy Rella', 'Alice Vunderlind'],
      newImage: '',
      images: [],
      isLoading: true
    }
  },
  methods: {
    addContact() {
      this.contacts.push(this.newContact)
      this.newContact = ''
    },
    sortContacts() {
      this.contacts.sort()
    },
    addImage() {
      this.images.push(this.newImage)
      this.newImage = ''
    },
    sortImages() {
      this.images.sort()
    }
  }
}
</script>

<style lang="scss" scoped>
.list-container {
  max-width: 1440px;
  margin: auto;
}

.gallery {
  width: 100%;
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(320px, 1fr));
  grid-gap: 5px;
  grid-auto-flow: dense;
  align-items: stretch;
  padding: 2rem;

  & .img-container {
    position: relative;
    width: 100%;
    height: 100%;
    cursor: pointer;
    box-shadow: 2px 2px 6px 0px rgba(0, 0, 0, 0.3);
    transition: transform 0.2s ease;

    &:hover {
      z-index: 1;
      transform: scale(1.05);
      transition: transform 0.2s ease;
    }

    &::before {
      content: '';
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background-color: rgba(0, 0, 0, 0);
      z-index: 1;
      transition: background-color 0.5s ease;
    }

    &:hover::before {
      background-color: rgba(0, 0, 0, 0.5);
      transition: background-color 0.5s ease;
    }

    & img {
      object-fit: cover;
      width: 100%;
      height: 100%;
    }

    @media screen and (min-width: 724px) {
      &:nth-child(4n + 4) {
        grid-column: span 2;
        grid-row: span 2;
      }
    }
  }
}
</style>
