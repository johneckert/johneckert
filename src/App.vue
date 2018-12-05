<template>
  <div id="app">
    <span id="my-name">John Eckert</span>
    <span id="my-job">Full Stack Developer</span>
    <vue-p5 @setup="setup" @draw="draw" @mouseclicked="handleClick"></vue-p5>
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
      t: 700,
      bgColor: "rgba(112, 128, 144, 0)",
      strokeColor: 0,
      strokeAlpha: 18, // 0 - 255
      clicked: false
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
      sketch.background(this.bgColor);
      sketch.stroke(this.strokeColor, this.strokeAlpha);
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

      //stop drawing after 5000 frames
      if (sketch.frameCount >= 5000) {
        sketch.frameRate(0);
      }
    },
    handleClick() {}
  }
};
</script>

<style>
@import url("https://fonts.googleapis.com/css?family=Anonymous+Pro");

body {
  background-color: rgb(112, 128, 144);
}

#app {
  width: 100vw;
  background-color: rgb(112, 128, 144);
}

#my-name {
  position: absolute;
  font-family: "Anonymous Pro", monospace;
  font-size: 2rem;
  color: rgb(112, 128, 144);
  left: 40%;
  top: 45%;
}

#my-job {
  position: absolute;
  font-family: "Anonymous Pro", monospace;
  font-size: 1rem;
  color: rgb(112, 128, 144);
  left: 45%;
  top: 50%;
}
</style>
