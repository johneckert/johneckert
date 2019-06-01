<template>
  <li class="link">
    <span v-on:click="toggleHidden">{{projectData.name}}</span>
    <transition name="slide">
      <div v-if="!hidden" class="project-tile">
        <h1 v-on:click="toggleHidden" class="close-button">X</h1>
        <h1>{{projectData.name}}</h1>
        <img :src="projectData.image"/>
        <div class="body">
          <h2>{{projectData.tagLine}}</h2>
          <h3 v-if="projectData.p1Title">{{projectData.p1Title}}</h3>
          <p v-if="projectData.p1">{{projectData.p1}}</p>
          <h3 v-if="projectData.p2Title">{{projectData.p2Title}}</h3>
          <p v-if="projectData.p2">{{projectData.p2}}</p>
          <h3 v-if="projectData.p3Title">{{projectData.p3Title}}</h3>
          <p v-if="projectData.p3">{{projectData.p3}}</p>
          <div class="proj-links">
            <a :href="projectData.gitHub">Github</a>
            <a :href="projectData.projLink">Try it!</a>
          </div>
        </div>
      </div>
      </transition>
  </li>
</template>

<script>

//NEED TO MOVE TRANSITION TO OUTER COMPONENT AND GIVE EACH LINK A CLICKED PROP THAT USES V-IF TO RENDER TILE
export default {
  name: "ProjectTile",
  props: {
    projectData: Object
  },
  data: function() {
    return {
      hidden: true
    }
  },
  methods: {
    toggleHidden: function() {
      this.hidden = !this.hidden
    }
  }
};
</script>

<style>
  .close-button {
    font-family: "Anonymous Pro", monospace;
    font-size: 1rem;
    color: #000000;
    float: right;
  }

  .link > span, .project-tile {
    font-family: "Anonymous Pro", monospace;
    font-size: 1rem;
    color: #000000;
  }

  .link > span:hover {
    color: white;
  }

  .body {
    overflow-y: scroll;
    height: 100%;
  }

  .project-tile {
    position: fixed;
    background-color: rgb(112, 128, 144);
    left: 10vw;
    height: 60vh;
    width: 80vw;
    padding: 2rem;
    border: solid 1px black;
    overflow: hidden;
    top: 10vh;
  }

  .proj-links {
    float: right;
  }

  .project-tile .proj-links a {
    margin-right: 50px;
    text-decoration: none;
    color: #000000;
  }

  .project-tile .proj-links a:visited {
    color: #BAC0C8;
  }

  .project-tile .proj-links a:hover, .close-button:hover {
    color: #ffffff;
  }

.slide-enter-active {
  transition: 1s;
}

.slide-leave-active {
  transition: 1s;
}

.slide-enter {
  transform: translate(0, 200%);
}
.slide-leave-to {
  transform: translate(0, 200%);
}
</style>