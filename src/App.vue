// src/App.vue
<template>
  <div id="app">
    <h1>Pendulum SVG Creator</h1>
    <PendulumSVGCreator />
  </div>
</template>

<script>
  import PendulumSVGCreator from "./components/PendulumSVGCreator.vue";

  export default {
    name: "App",
    components: {
      PendulumSVGCreator,
    },
  };
</script>

<style>
  #app {
    font-family: Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }
</style>
