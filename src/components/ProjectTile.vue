<template>
  <div class="project-tile">
    <h1>{{projectData.name}}</h1>
    <img :src="projectData.image"/>
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
</template>

<script>
export default {
  name: "ProjectTile",
  props: {
    projectData: Object
  }
};
</script>

<style>
</style>