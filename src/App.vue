<template>
  <div class="app">
    <h1>Rive Animation Demo</h1>

    <!-- Example using a public Rive file -->
    <RiveAnimation
      src="https://cdn.rive.app/animations/vehicles.riv"
      :width="500"
      :height="500"
      :autoplay="true"
      @load="onRiveLoad"
      @loaderror="onRiveError"
    />

    <p class="info">
      Replace the src with your own .riv file URL or path
    </p>
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
