<template>
  <div id="app">
    <vue-p5 v-on="{setup}"></vue-p5>
  </div>
</template>

<script>
import VueP5 from "vue-p5";

export default {
  name: "app",
  components: {
    vueP5: VueP5
  },
  methods: {
    setup(sketch) {
      sketch.background("green");
      sketch.text("Hello p5!", 20, 20);
    }
  }
};
</script>

<style>
#app {
  width: 100vw;
}
</style>
