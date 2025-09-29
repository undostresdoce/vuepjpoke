<template>
  <div class="app">
    <HomeView />
    <Footer />
  </div>
</template>

<script>
// Importamos la vista principal y el footer
import HomeView from './views/HomeView.vue'
import Footer from './components/Footer.vue'

export default {
  name: 'App',
  components: {
    HomeView,
    Footer
  }
}
</script>

<style>
.app {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}
</style>
