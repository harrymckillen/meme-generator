<template>
  <div class="footer">
    <p>&copy; {{ text }}, {{currentYear}}</p>
  </div>
</template>

<script>
export default {
  name: 'Footer',
  props: {
    text: String
  },
  computed: {
    currentYear: function () {
      return new Date().getFullYear();
    }
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
