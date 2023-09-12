<template>
  <div id="app">
    <link-area
      id="bottom-links"
      ref="bottomLinks"
      :links="projects"
      :popup="false"
      :position="position.bottom"
    ></link-area>
    <link-area
      id="side-links"
      ref="sideLinks"
      :links="sideLinks"
      :popup="false"
      :position="position.side"
    ></link-area>
    <div id="name-area" ref="nameArea">
      <span id="my-name">Dumb Shit</span>
      <span id="my-job">by John Eckert</span>
    </div>
    <vue-p5 id="name-canvas" @setup="setup" @draw="draw"></vue-p5>
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
      position: {
        side: "side",
        bottom: "bottom"
      },
      nameAreaStyles: {},
      fr: 400, //default is 60
      xTitle: -4000,
      xLink: 7000,
      yLink: -5000,
      bgColor: "rgba(112, 128, 144, 0)",
      strokeColors: [
        "#05878a", // light teal
        "#074e67", // dark teal
        "#5a175d", // magenta 1
        "#67074e", // magenta 2
        "#dd9933", // saffron
        "#bfcf45", // mello yellow
        "#ec0faa", // hot pink
        "#2bf618" // lime
      ],
      barColor: "#393D47", // dark grey
      strokeAlpha: 255, // 0 - 255,
      strokeWeight: 6,
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
  methods: {
    handleResize() {
      this.window.width = window.innerWidth;
      this.window.height = window.innerHeight;
    },
    randomColor() {
      const randomIndex = Math.floor(Math.random() * this.strokeColors.length);
      return this.strokeColors[randomIndex];
    },
    setup(sketch) {
      let randomColor = this.randomColor();
      sketch.createCanvas(this.window.width, this.window.height);
      sketch.background(this.bgColor);
      sketch.stroke(randomColor);
      sketch.strokeWeight(this.strokeWeight);
      sketch.fill(randomColor);
      sketch.frameRate(this.fr);
    },
    draw(sketch) {
      let x1, y, x2;
      x1 = Math.random() * this.window.width - Math.random() * 500;
      x2 = x1 + Math.random() * this.window.width;
      y = this.window.height * Math.random();

      sketch.line(x1, y, x2, y);

      sketch.stroke(this.barColor);
      sketch.fill(this.barColor);

      // title rectangle
      let titleRectWidth = 800;
      let titleRectHeight = 100;

      sketch.rect(
        this.xTitle,
        this.window.height * 0.65,
        titleRectWidth,
        titleRectHeight
      );

      if (this.xTitle < -10) {
        this.xTitle += 10;
      }

      // bottom links rectangle
      let bottomLinkRectWidth = 1200;
      let bottomLinkRectHeight = 75;
      sketch.rect(
        this.xLink,
        this.window.height * 0.8,
        bottomLinkRectWidth,
        bottomLinkRectHeight
      );

      if (this.xLink > this.window.width - bottomLinkRectWidth) {
        this.xLink -= 10;
      }

      // side links rectangle
      let sideLinkRectWidth = 75;
      let sideLinkRectHeight = 500;
      sketch.rect(
        this.window.width * 0.9,
        this.yLink,
        sideLinkRectWidth,
        sideLinkRectHeight
      );

      if (this.yLink < -10) {
        this.yLink += 10;
      }

      // set color for next loop
      let randomColor = this.randomColor();
      sketch.stroke(randomColor);
      sketch.fill(randomColor);
    }
  }
};
</script>

<style>
@import url("https://fonts.googleapis.com/css?family=Anonymous+Pro");

body {
  background-color: rgb(249, 246, 238);
  overflow: hidden;
  margin: 0;
}

#app {
  width: 100vw;
  height: 100vh;
  position: absolute;
  background-color: rgb(249, 246, 238);
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
  left: 20%;
  top: 65%;
  padding-top: 8px;
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
</style>
