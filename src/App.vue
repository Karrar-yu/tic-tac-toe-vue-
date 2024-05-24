<template>
  <div id="app">
    <board />
  </div>
</template>

<script>
import board from "./components/Board.vue";

export default {
  components: {
    board,
  },
};
</script>

<style>
#app {
  max-width: 1280px;
  margin: 0 auto;
  padding: 2rem;
  text-align: center;
}

:root {
  font-family: Inter, system-ui, Avenir, Helvetica, Arial, sans-serif;
  line-height: 1.5;
  font-weight: 400;

  color-scheme: light dark;
  background: linear-gradient(-45deg, #491505, #6d0f33, #602020, #467504);
  background-size: 400% 400%;
  animation: gradient 15s ease infinite;
  height: 100vh;

  font-synthesis: none;
  text-rendering: optimizeLegibility;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

@keyframes gradient {
  0% {
    background-position: 0% 50%;
  }
  50% {
    background-position: 100% 50%;
  }
  100% {
    background-position: 0% 50%;
  }
}
</style>
