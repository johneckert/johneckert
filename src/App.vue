<template>
  <div id="app">
    <link-area id="bottom-links" ref="bottomLinks" :links="bottomLinks" :position="bottomLinkPos()"></link-area>
    <link-area id="side-links" ref="sideLinks" :links="sideLinks" :position="sideLinkPos()"></link-area>
    <div id="name-area" ref="nameArea" :style="namePos()">
      <span id="my-name">John Eckert</span>
      <span id="my-job">Full Stack Developer</span>
    </div>
    <!-- <project-tile :projectData="projects.duckie"></project-tile> -->
    <vue-p5 id="name-canvas" @setup="setup" @draw="draw" @mouseclicked="handleClick"></vue-p5>
  </div>
</template>

<script>
import VueP5 from "vue-p5";
import LinkArea from "@/components/LinkArea.vue";
import ProjectTile from "@/components/ProjectTile.vue"

export default {
  name: "app",
  components: {
    vueP5: VueP5,
    linkArea: LinkArea,
    projectTile: ProjectTile
  },
  data() {
    return {
      window: {
        width: 0,
        height: 0
      },
      nameAreaStyles: {},
      fr: 100, //default is 60
      t: 700,
      bgColor: "rgba(112, 128, 144, 0)",
      strokeColor: 0,
      strokeAlpha: 100, // 0 - 255,
      strokeWeight: 4,
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
          text: "Medium",
          icon: "medium",
          prefix: "fab",
          url: "https://medium.com/@johnteckert"
        },
        {
          text: "Email Me",
          icon: "envelope",
          prefix: "fas",
          url: "mailto:johnteckert@gmail.com"
        }
      ],
      bottomLinks: [
        {
          text: "Duckie",
          icon: "",
          url: "https://duckie.herokuapp.com/"
        },
        {
          text: "Dr. Meowio",
          icon: "",
          url: "http://dr-meowio.herokuapp.com/"
        },
        {
          text: "Magic 8 Ball",
          icon: "",
          url: "https://johneckert.github.io/MagicEightBall/index"
        },
        {
          text: "Gusty",
          icon: "",
          url: "https://itsgusty.herokuapp.com/"
        }
      ],
      projects: {
        duckie: {
          name: "Duckie",
          image: "",
          tagLine: "Are you stuck? Talk to the duck!",
          p1Title: "",
          p1: "Duckie is a React app that uses the JavaScript Web Speech API and Watson’s Natural Language API to create a Rubber Duck Debugger that can help users to get unstuck and identify gaps in their knowledge.",
          p2Title: "DASHBOARD",
          p2: "After logging in, the user has access to their dashboard which displays the number of conversations that they have had with Duckie as well as a visual representation of the keywords that have been most frequent across all of their conversations. The size of each word's bubble is determined by the importance of the keyword.",
          p3Title: "CONVERSATION",
          p3: "On the conversation page, the user can click a button to begin their conversation with Duckie. As they talk, Duckie uses the Web Speech API to render a transcript of their conversation to the page. That transcript is also sent to the backend where the Watson Natural Language API is used to generate keywords. As new keywords are returned Duckie displays the five most relevant at the bottom of the conversation page, as well as coloring those words in the transcript to match their corresponding bubble.",
          gitHub: "https://github.com/johneckert/duckie-frontend",
          projLink: "https://duckie.herokuapp.com/"
        }
      }
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
      areaWidth = this.$refs.bottomLinks ? this.$refs.bottomLinks.clientWidth : 0;
      autoCenter = this.window.width / 3 - areaWidth + "px";
      return autoCenter;
    },
    centerLinksV() {
      let areaHeight, autoCenter;
      areaHeight = this.$refs.bottomLinks ? this.$refs.bottomLinks.clientHeight : 0;
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
      sketch.stroke(this.strokeColor, this.strokeAlpha);
      sketch.strokeWeight(this.strokeWeight);
      sketch.noFill();
      sketch.frameRate(this.fr);
    },
    draw(sketch) {
      let x1, y1, x2, y2, x3, y3, x4, y4;
      x1 = this.window.width * sketch.noise(this.t + this.window.width * 70); // * 0 here will make it a diagonal
      y1 = this.window.height * sketch.noise(this.t + this.window.height * 40); // * 0 here will make it a diagonal
      x2 = this.window.width * sketch.noise(this.t + this.window.width * 20);
      y2 = this.window.height * sketch.noise(this.t + this.window.height * 50);
      x3 = this.window.width * sketch.noise(this.t + this.window.width * 80);
      y3 = this.window.height * sketch.noise(this.t + this.window.height * 10);
      x4 = this.window.width * sketch.noise(this.t + this.window.width * 50);
      y4 = this.window.height * sketch.noise(this.t + this.window.height * 20);

      sketch.bezier(x1, y1, x2, y2, x3, y3, x4, y4);

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
  background-color: rgb(112, 128, 144);
  overflow: hidden;
}

#app {
  width: 100vw;
  background-color: rgb(112, 128, 144);
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
  font-size: 2rem;
  color: rgb(112, 128, 144);
}

#my-job {
  font-family: "Anonymous Pro", monospace;
  font-size: 1rem;
  color: rgb(112, 128, 144);
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
