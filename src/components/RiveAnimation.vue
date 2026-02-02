<template>
  <canvas ref="canvas" :width="width" :height="height"></canvas>
</template>

<script>
import { Rive } from '@rive-app/canvas';

export default {
  name: 'RiveAnimation',
  props: {
    src: {
      type: String,
      required: true
    },
    stateMachines: {
      type: [String, Array],
      default: null
    },
    animations: {
      type: [String, Array],
      default: null
    },
    autoplay: {
      type: Boolean,
      default: true
    },
    fit: {
      type: String,
      default: 'contain' // contain, cover, fill, fitWidth, fitHeight, none, scaleDown
    },
    alignment: {
      type: String,
      default: 'center' // center, topLeft, topCenter, topRight, centerLeft, centerRight, bottomLeft, bottomCenter, bottomRight
    },
    width: {
      type: Number,
      default: 400
    },
    height: {
      type: Number,
      default: 400
    }
  },
  emits: ['load', 'loaderror', 'play', 'pause', 'stop', 'statechange'],
  data() {
    return {
      rive: null
    };
  },
  mounted() {
    this.initRive();
  },
  beforeUnmount() {
    this.cleanup();
  },
  methods: {
    initRive() {
      const options = {
        src: this.src,
        canvas: this.$refs.canvas,
        autoplay: this.autoplay,
        onLoad: () => {
          this.$emit('load', this.rive);
        },
        onLoadError: (err) => {
          this.$emit('loaderror', err);
        },
        onPlay: () => {
          this.$emit('play');
        },
        onPause: () => {
          this.$emit('pause');
        },
        onStop: () => {
          this.$emit('stop');
        },
        onStateChange: (event) => {
          this.$emit('statechange', event);
        }
      };

      // Add state machines if provided
      if (this.stateMachines) {
        options.stateMachines = Array.isArray(this.stateMachines)
          ? this.stateMachines
          : [this.stateMachines];
      }

      // Add animations if provided (used when not using state machines)
      if (this.animations) {
        options.animations = Array.isArray(this.animations)
          ? this.animations
          : [this.animations];
      }

      this.rive = new Rive(options);
    },
    cleanup() {
      if (this.rive) {
        this.rive.cleanup();
        this.rive = null;
      }
    },
    // Exposed methods for parent components
    play(names) {
      if (this.rive) this.rive.play(names);
    },
    pause(names) {
      if (this.rive) this.rive.pause(names);
    },
    stop(names) {
      if (this.rive) this.rive.stop(names);
    },
    reset() {
      if (this.rive) this.rive.reset();
    }
  },
  watch: {
    src() {
      this.cleanup();
      this.initRive();
    }
  }
};
</script>

<style scoped>
canvas {
  display: block;
}
</style>
