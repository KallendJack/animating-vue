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
        'https://source.unsplash.com/400x400/?sea',
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

<style scoped>
.list-container {
  max-width: 1200px;
  margin: auto;
}
.image-list {
  width: 100%;
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(320px, 1fr));
  grid-gap: 20px;
  padding: 2rem;
}

.image-list img {
  width: 100%;
  height: 100%;
  min-width: 320px;
  box-shadow: 3px 3px 1px #ccc;
  -webkit-box-shadow: 3px 3px 1px #ccc;
  -moz-box-shadow: 3px 3px 1px #ccc;
}

.image-list li {
  position: relative;
  z-index: 1;
  height: 100%;
  cursor: pointer;
  transition: transform 0.5s ease;
}

.image-list li:hover {
  transform: scale(1.05);
  transition: transform 0.5s ease;
}
</style>
