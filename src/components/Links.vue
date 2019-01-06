<template>
  <vue-p5 id="link-canvas" @setup="setup" @draw="draw"></vue-p5>
</template>

<script>
import VueP5 from "vue-p5";

export default {
  name: "Links",
  components: {
    vueP5: VueP5
  },
  props: {
    width: {
      type: Number,
      default: 0
    },
    height: {
      type: Number,
      default: 0
    }
  },
  computed: {
    linkWidth: () => this.width / 4
  },
  methods: {
    setup(sketch) {
      sketch.movers = [];
      sketch.createCanvas(this.width, this.height);
      reset();
      function Mover(m, x, y) {
        this.mass = m;
        this.position = sketch.createVector(x, y);
        this.velocity = sketch.createVector(0, 0);
        this.acceleration = sketch.createVector(0, 0);
        this.applyForce = function(force) {
          var f = force.div(this.mass);
          this.acceleration.add(f);
        };
        this.update = function() {
          // Velocity changes according to acceleration
          this.velocity.add(this.acceleration);
          // position changes by velocity
          this.position.add(this.velocity);
          // We must clear acceleration each frame
          this.acceleration.mult(0);
        };
        this.display = function() {
          sketch.stroke(0);
          sketch.strokeWeight(2);
          sketch.fill(255, 127);
          sketch.ellipse(
            this.position.x,
            this.position.y,
            this.mass * 16,
            this.mass * 16
          );
        };
        this.checkEdges = function() {
          if (this.position.y > sketch.height - this.mass * 8) {
            // A little dampening when hitting the bottom
            this.velocity.y *= -0.9;
            this.position.y = sketch.height - this.mass * 8;
          }
        };
      }
      function reset() {
        for (var i = 0; i < 5; i++) {
          sketch.movers[i] = new Mover(3 + i * 0.1, 40 + i * 70, 0);
        }
      }
    },
    draw(sketch) {
      sketch.clear();
      for (let i = 0; i < sketch.movers.length; i++) {
        // Gravity is scaled by mass here!
        var gravity = sketch.createVector(0, 3 * sketch.movers[i].mass);
        // Apply gravity
        sketch.movers[i].applyForce(gravity);
        // Update and display
        sketch.movers[i].update();
        sketch.movers[i].display();
        sketch.movers[i].checkEdges();
      }
    }
  }
};
</script>


<style>
#link-canvas {
  width: 25vw;
  height: 90vh;
  position: absolute;
  right: 5vw;
  top: -2vh;
  padding-bottom: 10rem;
}
</style>
