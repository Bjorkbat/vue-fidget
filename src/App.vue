<template>
  <div id="app">
    <object type="image/svg+xml" data="/src//assets/11OnlineFidget.svg"
      width="200" height="200"
        v-bind:style="{transform: rotation}">
    </object>
    <button v-on:click="spin">
      Spin
    </button>
  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      acceleration: 0,
      velocity: 0,
      angle: 0,
      friction: 0.5
    }
  },

  computed: {

    rotation: function() {
      return "rotate(" + this.angle + "deg)";
    }
  },

  methods: {

    spin: function() {

      this.acceleration += 5;
      if (this.velocity <= 0) {
        this.update();
      }

    },

    update: function() {

      this.velocity = this.velocity + this.acceleration - this.friction;
      if (this.acceleration > 0) {
        this.acceleration -= this.friction;
      }
      this.angle += this.velocity;

      if (this.velocity > 0) {
        requestAnimationFrame(this.update);
      }

    }

  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
