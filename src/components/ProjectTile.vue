<template>
  <li class="link">
    <span v-on:click="toggleHidden">{{projectData.name}}</span>
    <div class="project-tile" :class="{hidden: hidden}">
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
        <a :href="projectData.gitHub">Github</a>
        <a :href="projectData.projLink">Try it!</a>
      </div>
    </div>
  </li>
</template>

<script>
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
  .hidden {
    display: none;
  }

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
    top: 10vh;
    left: 10vw;
    width: 80vw;
    height: 60vh;
    padding: 2rem;
    border: solid 1px black;
    overflow: hidden;
  }

</style>