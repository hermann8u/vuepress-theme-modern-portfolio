<template>
  <div v-if="socials.length" class="socials">
    <a v-for="social in socials" :href="social.link" target="_blank" rel="noopener noreferrer">
      <FaIcon :icon="social.icon" class="fa-2x"/>
    </a>
  </div>
</template>

<script>
import FaIcon from './FaIcon.vue'

export default {
  components: { FaIcon },
  computed: {
    socials () {
      return this.$site.themeConfig.socials || [];
    }
  }
}
</script>

<style lang="scss" scoped>
@import '../scss/config';
@import '../scss/mixins';

.socials {
  a {
    padding: 0.4rem;
    color: set-text-color($main-color);

    &:hover {
      color: $accent-color;
      @include easeOut();
    }
  }
}

@include mediaMd {
  .socials {
    text-align: center;
  }
}
</style>
