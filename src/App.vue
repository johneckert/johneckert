<template>
  <div id="app">
    <link-area
      id="bottom-links"
      ref="bottomLinks"
      :links="projects"
      :position="bottomLinkPos()"
      :popup="false"
    ></link-area>
    <link-area
      id="side-links"
      ref="sideLinks"
      :links="sideLinks"
      :position="sideLinkPos()"
      :popup="false"
    ></link-area>
    <div id="name-area" ref="nameArea" :style="namePos()">
      <span id="my-name">John Eckert</span>
      <span id="my-job">Full Stack Developer</span>
    </div>
    <!-- <project-tile :projectData="projects.duckie"></project-tile> -->
    <vue-p5
      id="name-canvas"
      @setup="setup"
      @draw="draw"
      @mouseclicked="handleClick"
    ></vue-p5>
  </div>
</template>

<script>
import VueP5 from "vue-p5";
import LinkArea from "@/components/LinkArea.vue";

export default {
  name: "app",
  components: {
    vueP5: VueP5,
    linkArea: LinkArea
  },
  data() {
    return {
      window: {
        width: 0,
        height: 0
      },
      nameAreaStyles: {},
      fr: 150, //default is 60
      t: 700,
      bgColor: "rgba(112, 128, 144, 0)",
      strokeColors: [
        "#67aec4",
        "#675682",
        "#5f0f4e",
        "#e52a6f",
        "#4a4646",
        "#27a284",
        "#dd9933"
      ],
      strokeAlpha: 255, // 0 - 255,
      strokeWeight: 3,
      clicked: false,
      sideLinks: [
        {
          text: "GitHub",
          icon: "github",
          prefix: "fab",
          url: "https://github.com/johneckert"
        },
        {
          text: "LinkedIn",
          icon: "linkedin",
          prefix: "fab",
          url: "https://www.linkedin.com/in/johnteckert/"
        },
        {
          text: "Resume",
          icon: "file",
          prefix: "fas",
          url: "https://standardresume.co/r/johneckert"
        },
        {
          text: "Email Me",
          icon: "envelope",
          prefix: "fas",
          url: "mailto:johnteckert@gmail.com"
        }
      ],
      projects: [
        {
          text: "Magic 8 Ball",
          url: "https://johneckert.github.io/MagicEightBall/index"
        },
        {
          text: "Tile Cascade",
          url: "http://johneckert.github.io/TileCascade/index"
        },
        {
          text: "Magic 8 Ball",
          url: "https://johneckert.github.io/MagicEightBall/index"
        },
        {
          text: "Tile Cascade",
          url: "http://johneckert.github.io/TileCascade/index"
        }
      ]
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
  mounted() {
    this.centerLinksH();
    this.centerLinksV();
  },
  methods: {
    handleResize() {
      this.window.width = window.innerWidth;
      this.window.height = window.innerHeight;
    },
    randomColor() {
      const randomIndex = Math.floor(
        Math.random(0, this.strokeColors.length) * 10
      );
      return this.strokeColors[randomIndex];
    },
    centerNameH() {
      let areaWidth, autoCenter;
      areaWidth = this.$refs.nameArea ? this.$refs.nameArea.clientWidth : 0;
      autoCenter = this.window.width / 2.5 - areaWidth + "px";
      return autoCenter;
    },
    centerNameV() {
      let areaHeight, autoCenter;
      areaHeight = this.$refs.nameArea ? this.$refs.nameArea.clientheight : 0;
      autoCenter = this.window.height / 2 - areaHeight + "px";
      return autoCenter;
    },
    centerLinksH() {
      let areaWidth, autoCenter;
      areaWidth = this.$refs.bottomLinks
        ? this.$refs.bottomLinks.clientWidth
        : 0;
      autoCenter = this.window.width / this.projects.length + "px";
      return autoCenter;
    },
    centerLinksV() {
      let areaHeight, autoCenter;
      areaHeight = this.$refs.bottomLinks
        ? this.$refs.bottomLinks.clientHeight
        : 0;
      autoCenter = this.window.height / 2 - areaHeight + "px";
      return autoCenter;
    },
    sideLinkPos() {
      return {
        top: 0,
        right: 0
      };
    },
    bottomLinkPos() {
      return {
        left: this.centerLinksH(),
        bottom: 0
      };
    },
    namePos() {
      return {
        left: this.centerNameH(),
        bottom: this.centerNameV()
      };
    },
    setup(sketch) {
      sketch.createCanvas(this.window.width, this.window.height);
      sketch.background(this.bgColor);
      sketch.stroke(this.randomColor());
      sketch.strokeWeight(this.strokeWeight);
      sketch.noFill();
      sketch.frameRate(this.fr);
    },
    draw(sketch) {
      let x1, y1, x2, y2, x3, y3, x4, y4;
      x1 = this.window.width * sketch.noise(this.t + this.window.width * 10); // * 0 here will make it a diagonal
      y1 = this.window.height * sketch.noise(this.t + this.window.height * 50); // * 0 here will make it a diagonal
      x2 = this.window.width * sketch.noise(this.t + this.window.width * 10);
      y2 = this.window.height * sketch.noise(this.t + this.window.height * 50);
      x3 = this.window.width * sketch.noise(this.t + this.window.width * 50);
      y3 = this.window.height * sketch.noise(this.t + this.window.height * 50);
      x4 = this.window.width * sketch.noise(this.t + this.window.width * 50);
      y4 = this.window.height * sketch.noise(this.t + this.window.height * 50);

      sketch.bezier(x1, y1, x2, y2, x3, y3, x4, y4);

      sketch.stroke(this.randomColor());

      this.t += 0.5;
      //stop drawing after 5000 frames
      if (sketch.frameCount >= 8000) {
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
  background-color: rgb(249, 246, 238);
  overflow: hidden;
}

#app {
  width: 100vw;
  background-color: rgb(249, 246, 238);
  /*background-color: rgb(112, 128, 144);*/
}

#name-canvas {
  overflow: hidden;
}

#name-area {
  position: absolute;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

#my-name {
  font-family: "Anonymous Pro", monospace;
  font-size: 3rem;
  color: rgb(249, 246, 238);
}

#my-job {
  font-family: "Anonymous Pro", monospace;
  font-size: 2rem;
  color: rgb(249, 246, 238);
}

#bottom-links {
  flex-direction: row;
  align-items: center;
  justify-content: center;
}

#side-links {
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding-top: 2em;
}

#bottom-links > .link {
  margin: 2em;
}

#side-links > .link {
  margin: 0.5em 2em;
}
</style>
