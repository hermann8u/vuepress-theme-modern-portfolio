<template>
  <div class="theme-container" :class="{ 'bg-img': hasBackgroundImage, 'no-overflow': isNavOpen }" :style="backgroundStyle">
    <Nav v-on:nav-open="isNavOpen = $event"/>
      <main>
        <transition mode="out-in" name="page">
          <Home v-if="pageType === 'home'"/>
          <Projects v-else-if="pageType === 'projects'"/>
          <About v-else-if="pageType === 'about'"/>
          <Header v-else />
        </transition>
        <transition mode="out-in" name="page">
          <Content/>
        </transition>
      </main>
      <Footer v-if="displayFooter"/>
  </div>
</template>

<script>
import Home from './components/Home.vue'
import Projects from './components/Projects.vue'
import About from './components/About.vue'
import Nav from './components/Nav.vue'
import Header from './components/Header.vue'
import Footer from './components/Footer.vue'
import FaIcon from './components/FaIcon.vue'

export default {
  components: { Home, Projects, About, Header, Nav, FaIcon, Footer },
  data () {
    return {
      isNavOpen: false
    }
  },
  computed: {
    hasBackgroundImage () {
      return this.pageType === 'home' || this.$page.frontmatter.hasBackgroundImage;
    },
    background () {
      return this.$site.themeConfig.background || null;
    },
    backgroundStyle () {
      return this.background && this.hasBackgroundImage ? { 'background-image': 'url(' + this.background + ')' } : {};
    },
    pageType () {
      return this.$page.frontmatter.pageType || null;
    },
    displayFooter () {
      if (this.$page.frontmatter.footer !== undefined && this.$page.frontmatter.footer.display !== undefined) {
        return this.$page.frontmatter.footer.display;
      }

      if (this.$site.themeConfig.footer !== undefined && this.$site.themeConfig.footer.display !== undefined) {
        return this.$site.themeConfig.footer.display;
      }

      return false;
    }
  }
}
</script>

<style src="./scss/theme.scss" lang="scss"></style>
<style lang="scss" scoped>
.page-enter-active, .page-leave-active {
  transition: opacity .5s;
}
.page-enter, .page-leave-to {
  opacity: 0;
}
</style>
