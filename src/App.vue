<template>
  <div id="app">
    <Header title="Meme Generator"/>
    <MemeGen />
    <Footer text="Sample Meme Generator"/>
  </div>
</template>

<script>
import Header from './components/Header.vue'
import MemeGen from './components/MemeGen.vue'
import Footer from './components/Footer.vue'

export default {
  name: 'App',
  components: {
    Header,
    MemeGen,
    Footer
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /* text-align: center; */
  /* color: #2c3e50; */
  margin: 0;
}
</style>
