<template>
  <div class="list-container">
    <input type="text" v-model="newContact" placeholder="Name" />
    <button @click="addContact">Add Contact</button>
    <button @click="sortContacts">Sort</button>

    <transition-group name="slide-up" tag="ul" appear>
      <li v-for="contact in contacts" :key="contact">
        {{ contact }}
      </li>
    </transition-group>

    <input type="text" v-model="newImage" placeholder="Name" />
    <button @click="addImage">Add Image</button>
    <button @click="sortImages">Sort</button>
    <transition-group name="slide-up" tag="ul" appear class="gallery">
      <img v-for="image in images" :key="image" :src="image" />
    </transition-group>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newContact: '',
      contacts: ['Beau Thabeast', 'Cindy Rella', 'Alice Vunderlind'],
      newImage: '',
      images: [
        'https://source.unsplash.com/400x400/?trees,water',
        'https://source.unsplash.com/400x400/?snow',
        'https://source.unsplash.com/400x400/?ice',
        'https://source.unsplash.com/400x400/?circus',
        'https://source.unsplash.com/400x400/?bike',
        'https://source.unsplash.com/400x400/?road'
      ]
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
  max-width: 1200px;
  margin: auto;
}

.gallery {
  width: 100%;
  height: auto;
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(320px, 1fr));
  grid-gap: 20px;
  align-items: center;
  padding: 2rem;

  & img {
    position: relative;
    z-index: 1;
    width: 100%;
    min-height: 320px;
    min-width: 320px;
    cursor: pointer;
    box-shadow: 2px 2px 6px 0px rgba(0, 0, 0, 0.3);
    transition: transform 0.5s ease;

    &:hover {
      transform: scale(1.05);
      transition: transform 0.5s ease;
    }

    @media screen and (min-width: 1065px) {
      &:nth-child(4) {
        grid-column: span 2;
        grid-row: span 2;
      }
    }
  }
}
</style>
