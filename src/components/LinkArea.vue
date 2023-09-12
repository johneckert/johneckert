<template>
  <div
    :class="[
      { linkAreaSide: position === 'side' },
      { linkAreaBottom: position === 'bottom' }
    ]"
    ref="linkArea"
  >
    <ul>
      <link-item v-for="(link, i) in links" :linkData="link" :key="i" />
    </ul>
  </div>
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
    popup: Boolean,
    position: String
  }
};
</script>

<style>
.linkAreaSide {
  position: absolute;
  padding-top: 2em;
  left: 90%;
  min-height: 100vh;
  width: 150px;
  max-width: 79px;
}

.linkAreaSide > ul {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: flex-start;
  list-style-type: none;
  margin: 0;
  padding: 0;
}

.linkAreaBottom {
  position: absolute;
  top: 80%;
  left: 0;
  min-width: 100vw;
}

.linkAreaBottom > ul {
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: center;
  list-style-type: none;
  margin: 0 0 0 20%;
  padding: 0;
}
</style>
