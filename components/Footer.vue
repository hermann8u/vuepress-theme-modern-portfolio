<template>
  <footer>
    {{ content }}
  </footer>
</template>

<script>
export default {
  computed: {
    content () {
      if (this.$page.frontmatter.footer !== undefined && this.$page.frontmatter.footer.content) {
        return this.$page.frontmatter.footer.content;
      }

      if (this.$site.themeConfig.footer !== undefined && this.$site.themeConfig.footer.content !== undefined) {
        return this.$site.themeConfig.footer.content;
      }

      return 'Copyright © ' + this.currentYear;
    },
    currentYear () {
      let date = new Date();

      return date.getFullYear();
    }
  }
}
</script>


<style lang="scss" scoped>
@import '../scss/config';
@import '../scss/mixins';

footer {
  position: relative;
  z-index: 2;
  text-align: center;
  padding: 1rem;
  background: darken($main-color, 10);
  color: set-text-color($main-color);
  height: 60px;
}
</style>
