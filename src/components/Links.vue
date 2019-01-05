<template>
  <div id="link-area">
    <vue-p5 id="link-canvas" @setup="setup" @draw="draw"></vue-p5>
  </div>
</template>

<script>
// import VueP5 from "vue-p5";

export default {
  name: "Links",
  components: {
    // vueP5: VueP5
  },
  props: {
    width: Number,
    height: Number
  },
  computed: {
    linkWidth: () => this.width / 3
  },
  methods: {
    setup(sketch) {
      sketch.createCanvas(this.linkWidth, this.height);
      sketch.frameRate(this.fr);
    },
    draw(sketch) {
      return sketch;
    }
  }
};
</script>


<style>
/* #link-canvas {
  position: absolute;
} */

#link-area {
  background-color: black;
  width: 25%;
  height: 100%;
  position: absolute;
  right: 0;
}
</style>
