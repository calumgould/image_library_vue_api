<template lang="html">
  <div class="sponsor-canvas">
    <canvas id="sponsorCanvas" width="700" height="100">Canvas not supported</canvas>
  </div>
</template>

<script>
export default {
  name: 'sponsor-canvas',
  props: ['canvas'],
  methods: {
    scrollCanvas() {
      var canvas = null;
      var context = null;
      var string = "Sponsored by ilma.";
      var startW = 250
      var startX = -startW;

      function init() {
        canvas = document.getElementById('sponsorCanvas');
        context = canvas.getContext('2d');

        blank();

        context.font = "25px Nunito";
        context.fillStyle = "black";
        context.fillText(string, startX, 55);

        requestAnimationFrame(anim)
      }

      function blank() {
        context.fillStyle = "lightgrey";
        context.fillRect(0, 0, context.canvas.width, context.canvas.height);
      }

      function anim(timestamp) {
        if (startX < context.canvas.width) {
          blank();
          startX += 5;
          context.font = "25px Nunito";
          context.fillStyle = "black";
          context.fillText(string, startX, 55)
        }
        else {
          startX = -startW;
        }

        requestAnimationFrame(anim)
      }

      window.addEventListener("load", init)
    }
  }
}
</script>

<style lang="css" scoped>
</style>
