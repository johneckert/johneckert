<template>
  <li class="link">
    <a href="linkUrl">{{text}}</a>
  </li>
</template>

<script>
export default {
  name: "Link",
  props: {
    text: String,
    url: String
  },
  computed: {},
  methods: {}
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
