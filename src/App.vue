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
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 40px;
}

h1 {
  margin-bottom: 20px;
}

.info {
  margin-top: 20px;
  color: #666;
  font-size: 14px;
}
</style>
