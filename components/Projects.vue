<template>
  <div>
    <Header/>
    <div v-if="projects" class="projects">
      <Project v-for="project in projects" :link="project.link" :github-link="project.githubLink" :image="project.image"/>
    </div>
  </div>
</template>

<script>
import Project from './Project.vue'
import Header from './Header.vue'

export default {
  components: { Project, Header },
  computed: {
    projects () {
      return this.$site.themeConfig.projects || [];
    }
  }
}
</script>

<style lang="scss" scoped>
@import '../scss/config';
@import '../scss/mixins';

// Work/Projects
.projects {
  display: grid;
  grid-gap: 0.7rem;
  grid-template-columns: repeat(3, 1fr);
}

// Widescreens
@include mediaXl {
  .projects {
    grid-template-columns: repeat(4, 1fr);
  }
}

// Desktops & Laptops
@include mediaLg {
  .projects {
    grid-template-columns: repeat(3, 1fr);
  }
}

// Tablets & Small Laptops
@include mediaMd {
  .projects {
    grid-template-columns: repeat(2, 1fr);
  }
}

// Smartphones
@include mediaSm {
  .projects {
    grid-template-columns: 1fr;
  }
}
</style>
