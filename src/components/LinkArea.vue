<template>
  <ul class="link-area" ref="linkArea" :style="linkAreaStyles">
    <link-item v-for="(link, i) in links" :url="link.url" :text="link.text" :key="i"/>
  </ul>
</template>

<script>
import Link from "@/components/Link.vue";
import Vue from "vue";

export default {
  name: "LinkArea",
  components: {
    linkItem: Link
  },
  data: function () {
      return {
          linkAreaStyles: {},
          window: {
            width: 0,
            height: 0
        }
      }
  },
  props: {
    links: Array
  },
  computed: {},
  methods: {
      centerLinks() {
        var areaWidth = this.$refs.linkArea.clientHeight;
        var autoCenter = this.window.width/2 - areaWidth + 'px';
        console.log(autoCenter, this.window.width, areaWidth)
        Vue.set(this.linkAreaStyles, 'left', autoCenter)
      },
      handleResize() {
      this.window.width = window.innerWidth;
      this.window.height = window.innerHeight;
    }
  },
  created() {
    window.addEventListener('resize', this.handleResize)
    this.handleResize();
  },
mounted() {
        this.centerLinks()
    },
destroyed() {
    window.removeEventListener('resize', this.handleResize)
  },
};
</script>


<style>
.link-area {
    position: absolute;
    bottom: 0;
    list-style-type: none;
    display: flex;
    margin:0;
    padding:0;
}
</style>
