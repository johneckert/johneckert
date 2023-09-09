<template>
  <li class="link">
    <a :href="linkData.url" target="_blank">
      <font-awesome-icon
        v-if="!!linkData.icon"
        :icon="[linkData.prefix, linkData.icon]"
        size="2x"
      />
      <span v-else>{{ linkData.text }}</span>
    </a>
  </li>
</template>

<script>
export default {
  name: "Link",
  props: {
    linkData: Object
  }
};
</script>

<style>
.link > a {
  font-family: "Anonymous Pro", monospace;
  font-size: 1rem;
  color: #000000;
}

.link > a:hover {
  color: white;
}
</style>
