<template>
  <div>
    <Header/>
    <div class="about-info">
      <Portrait/>
      <div class="bio">
        <h2 v-if="bioTitle" class="text-accent">{{ bioTitle }}</h2>
        <div class="bio-content">
          <p v-for="bioItem in bioContent">
            {{ bioItem }}
          </p>
        </div>
      </div>
    </div>
     <h2 v-if="itemsTitle" class="text-accent mb-1">{{ itemsTitle }}</h2>
     <div class="grid-items">
      <GridItem v-for="item in items" :hasHeadingTitle="hasHeadingTitle" :title="item.title" :subtitle="item.subtitle" :content="item.content"/>
    </div>
  </div>
</template>

<script>
import Portrait from './Portrait.vue'
import Header from './Header.vue'
import GridItem from './GridItem.vue'

export default {
  components: { Portrait, Header, GridItem },
  computed: {
    bioTitle () {
      return this.$page.frontmatter.bio.title || null;
    },
    bioContent () {
      if (!this.$page.frontmatter.bio) {
        return null;
      }

      if (typeof this.$page.frontmatter.bio == 'string') {
        return [this.$page.frontmatter.bio];
      }

      if (typeof this.$page.frontmatter.bio == 'object' && this.$page.frontmatter.bio[0]) {
        return this.$page.frontmatter.bio;
      }

      if (!this.$page.frontmatter.bio.content) {
        return null;
      }

      if (typeof this.$page.frontmatter.bio.content == 'string') {
        return [this.$page.frontmatter.bio.content];
      }

      if (typeof this.$page.frontmatter.bio.content == 'object' && this.$page.frontmatter.bio.content[0]) {
        return this.$page.frontmatter.bio.content;
      }
    },
    itemsTitle () {
      return this.$page.frontmatter.itemsTitle || null;
    },
    items () {
      return this.$page.frontmatter.items || null;
    },
    hasHeadingTitle () {
      return typeof this.itemsTitle === 'string';
    }
  }
}
</script>

<style lang="scss">
@import '../scss/config';
@import '../scss/mixins';

h2 {
  font-size: 2rem;
}

.about-info {
  margin-bottom: 2rem;
  display: grid;
  grid-gap: 30px;
  grid-template-areas: 'portrait bio';
  grid-template-columns: 1fr 2fr;

  .portrait {
    grid-area: portrait;
    margin: auto;
  }

  .bio {
    grid-area: bio;
    font-size: 1.5rem;
    text-align: justify;
  }
}

.grid-items {
  margin-bottom: 2rem;
  display: grid;
  grid-gap: 30px;
  grid-template-columns: repeat(3, 1fr);
}

@include mediaMd {
  .about-info {
    grid-template-areas: 'portrait' 'bio';
    grid-template-columns: 1fr;
  }

  .grid-items {
    grid-template-columns: 1fr;
  }
}
</style>
