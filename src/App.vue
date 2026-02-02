<template>
  <div class="app">
    <h1>Rive Animation Demo</h1>

    <RiveAnimation
      src="/orb_particles.riv"
      :width="500"
      :height="500"
      :autoplay="true"
      @load="onRiveLoad"
      @loaderror="onRiveError"
    />
  </div>
</template>

<script>
import RiveAnimation from './components/RiveAnimation.vue'

export default {
  name: 'App',
  components: {
    RiveAnimation
  },
  methods: {
    onRiveLoad(rive) {
      console.log('Rive animation loaded!', rive);
    },
    onRiveError(err) {
      console.error('Failed to load Rive animation:', err);
    }
  }
}
</script>

<style>
html, body {
  margin: 0;
  padding: 0;
  height: 100%;
  background-color: #222;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  background-color: #222;
  color: #e0e0e0;
}

h1 {
  margin-bottom: 30px;
  color: #ffffff;
  font-weight: 300;
}
</style>
