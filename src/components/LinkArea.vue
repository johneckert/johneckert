<template>
  <ul v-if="popup" class="link-area" ref="linkArea" :style="position">
    <project-tile v-for="(link, i) in links" :projectData="link" :key="i" />
  </ul>
  <ul v-else class="link-area" ref="linkArea" :style="position">
    <link-item v-for="(link, i) in links" :linkData="link" :key="i"/>
  </ul>
</template>

<script>
import Link from "@/components/Link.vue";
import ProjectTile from "@/components/ProjectTile.vue";

export default {
  name: "LinkArea",
  components: {
    linkItem: Link,
    projectTile: ProjectTile
  },
  props: {
    links: Array,
    position: Object,
    popup: Boolean
  }
};
</script>

<style>
.link-area {
  position: absolute;
  list-style-type: none;
  display: flex;
  margin: 0;
  padding: 0;
}
</style>
