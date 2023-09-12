<template>
  <li v-if="!!linkData.icon" class="link icon-link">
    <div class="spacer">
      <a :href="linkData.url" target="_blank">
        <font-awesome-icon :icon="[linkData.prefix, linkData.icon]" size="2x" />
      </a>
    </div>
  </li>
  <li v-else class="link text-link">
    <a :href="linkData.url" target="_blank">
      <span>{{ linkData.text }}</span>
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
.link a {
  font-family: "Anonymous Pro", monospace;
  font-size: 1.3rem;
  text-decoration: none;
  color: rgb(249, 246, 238);
}

.spacer {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 1.6rem;
  height: 1.6rem;
  margin-bottom: 1rem;
}

.icon-link {
  justify-self: center;
  margin: 1em;
}

.icon-link a:hover {
  font-size: 1.6rem;
  transition: font-size 0.3s linear;
}

.text-link {
  padding: 21px;
  margin: 0.5em;
}

.text-link:hover {
  padding: 15px;
  border: 6px solid rgb(249, 246, 238);
  border-radius: 50%;
  transition: border-style 0.6s linear;
}
</style>
