<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">Modal</router-link> |
      <router-link to="/list">List</router-link> |
      <router-link to="/drawer">Drawer</router-link> |
      <router-link to="/cards">Cards</router-link>
    </div>
    <transition name="slide-fade" mode="out-in">
      <router-view />
    </transition>
  </div>
</template>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

button {
  height: 2.2em;
  margin: 0.5em;
  border-radius: 0.3em;
  background: linear-gradient(to right, #16c0b0, #84cf6a);
  color: white;
}

input {
  display: inline-block;
  box-sizing: border-box;
  width: 30%;
  height: 1.8em;
  padding: 0.5em;
  margin: 0.2em;
  font: 0.8em 'Avenir', Helvetica, sans-serif;
}

.modal {
  width: 250px;
  height: 200px;
  padding: 10px;
  margin: 0 auto;
  margin-top: 20px;
  border-radius: 2%;
  background-color: #e0e0e0;
}

#nav {
  background-color: #586BA4;
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: white;
}

#nav a.router-link-exact-active {
  color: #42b983;
}

p {
  font-size: 0.8em;
}

::placeholder {
  color: #2c3e50;
}

ul {
  list-style-type: none;
}

/*** TRANSITIONS ***/
.fade-enter {
  opacity: 0;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s ease-out;
}

.fade-leave-to {
  opacity: 0;
}

.slide-fade-enter {
  transform: translateX(10px);
  opacity: 0;
}

.slide-fade-enter-active,
.slide-fade-leave-active {
  transition: all 0.2s ease;
}

.slide-fade-leave-to {
  transform: translateX(-10px);
  opacity: 0;
}

.slide-up-enter {
  transform: translateY(10px);
  opacity: 0;
}

.slide-up-enter-active {
  transition: all 1s ease;
}

/* Comes with transition-groups */
.slide-up-move {
  transition: transform 0.8s ease-in;
}
</style>
