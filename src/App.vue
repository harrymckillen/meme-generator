<template>
  <div id="app">
    <Header v-bind:title="title"/>
    <MemeGen />
    <Footer v-bind:text="title"/>
  </div>
</template>

<script>
import Header from './components/Header.vue'
import MemeGen from './components/MemeGen.vue'
import Footer from './components/Footer.vue'

export default {
  name: 'App',
  data(){
    return {
      title: 'Simple Meme Generator'
    }
  },
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
