<template>
  <li class="link">
    <a :href="linkData.url" target="_blank">{{linkData.text}}</a>
  </li>
</template>

<script>
export default {
  name: "Link",
  props: {
    linkData: Object
  },
  computed: {},
  methods: {},
  mounted() {
    console.log(this.url)
  }
};
</script>


<style>
.link > a {
  font-family: "Anonymous Pro", monospace;
  font-size: 1rem;
  color: #000000;
}

.link {
  margin: 2em;
}
</style>
