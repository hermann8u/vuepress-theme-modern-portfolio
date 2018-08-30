<template>
  <div class="item">
    <a :href="link">
      <img :src="image" alt="Project">
    </a>
    <a v-if="link" :href="link" target="_blank" rel="noopener noreferrer" class="btn-light">
      <FaIcon icon="eye"/> Project
    </a>
    <a v-if="githubLink" :href="githubLink" target="_blank" rel="noopener noreferrer" class="btn-dark">
      <FaIcon icon="github"/> Github
    </a>
  </div>
</template>

<script>
import FaIcon from './FaIcon.vue'

export default {
  components: { FaIcon },
  props: {
    image: {
      type: String,
      required: true
    },
    link: {
      type: String,
      required: false
    },
    githubLink: {
      type: String,
      required: false
    }
  }
}
</script>

<style lang="scss" scoped>
@import '../scss/config';
@import '../scss/mixins';

img {
  width: 100%;
  border: 3px #fff solid;

  &:hover {
    opacity: 0.5;
    border-color: $accent-color;
    @include easeOut;
  }
}
</style>

