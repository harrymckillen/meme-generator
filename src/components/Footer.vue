<template>
  <div class="footer">
    <p>&copy; {{ text }}</p>
  </div>
</template>

<script>
export default {
  name: 'Footer',
  props: {
    text: String
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .footer {
    display: block;
    padding: 2em 0;
    font-family: Arial, Helvetica, sans-serif;
    text-align: center;
  }
</style>
