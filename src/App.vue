<template>
  <div id="app">
    <vue-p5 @setup="setup" @draw="draw"></vue-p5>
  </div>
</template>

<script>
import VueP5 from "vue-p5";

export default {
  name: "app",
  components: {
    vueP5: VueP5
  },
  data() {
    return {
      width: 0,
      height: 0,
      t: 100
    };
  },
  created() {
    //get window dimensions live
    window.addEventListener("resize", this.handleResize);
    this.handleResize();
  },
  destroyed() {
    window.removeEventListener("resize", this.handleResize);
  },
  methods: {
    handleResize() {
      this.width = window.innerWidth;
      this.height = window.innerHeight;
    },
    setup(sketch) {
      sketch.createCanvas(this.width, this.height);
      sketch.background(112, 128, 144);
      sketch.stroke(0, 18);
      sketch.noFill();
    },
    draw(sketch) {
      let x1 = this.width * sketch.noise(this.t + this.width * 0);
      let x2 = this.width * sketch.noise(this.t + this.width * 5);
      let x3 = this.width * sketch.noise(this.t + this.width * 10);
      let x4 = this.width * sketch.noise(this.t + this.width * 20);
      let y1 = this.height * sketch.noise(this.t + this.height * 0);
      let y2 = this.height * sketch.noise(this.t + this.height * 5);
      let y3 = this.height * sketch.noise(this.t + this.height * 10);
      let y4 = this.height * sketch.noise(this.t + this.height * 20);

      sketch.bezier(x1, y1, x2, y2, x3, y3, x4, y4);

      this.t += 0.5;

      // clear the background every 500 frames using mod (%) operator
      if (sketch.frameCount % 5000 == 0) {
        //will it ever crash if I don't clear?
        // sketch.background(112, 128, 144);
      }
    }
  }
};
</script>

<style>
#app {
  width: 100vw;
}
</style>
