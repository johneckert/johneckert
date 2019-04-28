<template>
  <ul class="link-area" ref="linkArea" :style="position">
    <link-item v-for="(link, i) in links" :linkData="link" :key="i"/>
  </ul>
</template>

<script>
import Link from "@/components/Link.vue";

export default {
  name: "LinkArea",
  components: {
    linkItem: Link
  },
  props: {
    links: Array,
    position: Object
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
