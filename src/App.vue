<template>
  <div class="app">
    <!-- <Navbar /> -->
    <map-item />
  </div>
</template>

<script>
// import Navbar from './components/Navbar.vue';
import MapItem from './Map.vue';

export default {
  name: 'App',
  components: {
    // Navbar,
    MapItem
  }
}
</script>

<style>
body {
  margin: 0;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', 'Roboto', 'Oxygen',
    'Ubuntu', 'Cantarell', 'Fira Sans', 'Droid Sans', 'Helvetica Neue',
    sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

code {
  font-family: source-code-pro, Menlo, Monaco, Consolas, 'Courier New',
    monospace;
}

.app {
  text-align: center;
}
</style>