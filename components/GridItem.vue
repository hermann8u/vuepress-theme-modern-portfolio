<template>
  <div class="grid-item">
    <h3 v-if="hasHeadingTitle">{{ title }}</h3>
    <h2 v-else>{{ title }}</h2>
    <div v-if="subtitle" class="item-subtitle">{{ subtitle }}</div>
    <div v-html="content"></div>
  </div>
</template>

<script>
export default {
  props: {
    hasHeadingTitle: {
      type: Boolean,
      required: false
    },
    title: {
      type: String,
      required: true
    },
    subtitle: {
      type: String,
      required: false
    },
    content: {
      type: String,
      required: false
    }
  }
}
</script>

<style scopped lang="scss">
@import '../scss/config';
@import '../scss/mixins';

.grid-item {
  background: lighten($main-color, 5);
  padding: 0.5rem;
  border-bottom: $accent-color 5px solid;
}

.item-subtitle {
  margin: 10px 0;
  font-size: 0.75em;
  font-weight: bold;
}
</style>