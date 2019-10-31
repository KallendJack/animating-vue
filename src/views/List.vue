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
    <transition-group name="slide-up" tag="ul" appear class="image-list">
      <li v-for="image in images" :key="image">
        <img :src="image" />
      </li>
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
        'https://source.unsplash.com/400x400/?lava'
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

<style scoped>
.list-container {
  margin: auto;
  padding: 0;
  box-sizing: border-box;
  max-width: 1200px;
}
.image-list {
  width: 100%;
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(320px, 1fr));
  grid-gap: 20px;
  margin: auto;
  padding: 0;
}

img {
  width: 100%;
  min-width: 320px;
}
</style>
