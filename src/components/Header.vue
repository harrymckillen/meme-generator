<template>
  <div class="header">
    <h1 class="text-2xl">{{ title }}</h1>
  </div>
</template>

<script>
export default {
  name: 'Header',
  props: {
    title: String
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .header {
    display: block;
    padding: 0.2em 1.5em;
    font-family: 'Anton', sans-serif;
    text-align: center;
  }
</style>
