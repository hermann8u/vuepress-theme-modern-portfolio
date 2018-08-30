<template>
  <header>
    <h1 class="lg-header">{{ firstheaderTitle }} <span v-if="secondheaderTitle" class="text-accent">{{ secondheaderTitle }}</span></h1>
    <div v-if="headerSubtitle" class="sm-header">{{ headerSubtitle }}</div>
  </header>
</template>

<script>
export default {
  computed: {
    firstheaderTitle () {
      return Array.isArray(this.$page.frontmatter.header.title) ? this.$page.frontmatter.header.title[0] : this.$page.frontmatter.header.title;
    },
    secondheaderTitle () {
      return Array.isArray(this.$page.frontmatter.header.title) && this.$page.frontmatter.header.title[1] ? this.$page.frontmatter.header.title[1] : null;
    },
    headerSubtitle () {
      return this.$page.frontmatter.header.subtitle || null;
    }
  }
}
</script>

<style scopped lang="scss">
@import '../scss/config';
@import '../scss/mixins';

header {
  margin-bottom: 2rem;
}

.lg-header {
  font-size: 6rem;
}

.sm-header {
  padding: 0.5rem 1rem;
  background: rgba(lighten($main-color, 2), 0.5);
  font-size: 1.5rem;
}

// Tablets & Small Laptops
@include mediaMd {
  .lg-header {
    font-size: 3rem;
    line-height: 1;
    margin-bottom: 1rem;
  }
  
  .sm-header, .lg-header {
    text-align: center;
  }
}
</style>