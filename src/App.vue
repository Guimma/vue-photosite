<template>
  <div id="app">
    <Navbar v-bind:currentAlbum="currentAlbum" @updateAlbum="updateAlbum"/>
    <Modal />
    <Photos v-bind:currentAlbum="currentAlbum" />
  </div>
</template>

<script>
import Photos from './components/Photos.vue'
import Navbar from './components/Navbar.vue'

export default {
  name: 'app',
  components: {
    Photos,
    Navbar
  },
  data: function(){
    return{
      currentAlbum: '0',
    }
  },
  methods: {
    updateAlbum(newAlbum) {
      this.currentAlbum = newAlbum;
    } 
  }
}
</script>

<style>
#app {
  margin: 0 auto;
}
</style>
