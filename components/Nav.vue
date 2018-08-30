<template>
  <nav>
    <NavButton @click.native="toggleNav" :isNavOpen="isNavOpen"/>
    <div class="menu" :class="{ show: isNavOpen}">
      <div class="menu-branding" :class="{ show: isNavOpen}">
        <Portrait/>
      </div>
      <ul class="menu-nav">
        <li v-for="page in navs" class="nav-item current">
          <router-link :to="page.link" class="nav-link" @click.native="toggleNav">{{ page.text }}</router-link>
        </li>
      </ul>
    </div>
  </nav>
</template>

<script>
import NavButton from './NavButton.vue'
import Portrait from './Portrait.vue'

export default {
  components: { NavButton, Portrait },
  data () {
    return {
      isNavOpen: false
    }
  },
  computed: {
    navs () {
      for (let nav of this.$site.themeConfig.nav) {
        if (this.$localePath !== '/' && !nav.link.startsWith(this.$localePath)) {
          nav.link = this.$localePath + nav.link.substring(1);
        }
      }

      return this.$site.themeConfig.nav;
    }
  },
  methods: {
    toggleNav() {
      this.isNavOpen = !this.isNavOpen;
      this.$emit('nav-open', this.isNavOpen);
    }
  }
}
</script>

<style scopped lang="scss">
@import '../scss/config';
@import '../scss/mixins';

nav {
  position: fixed;
  z-index: 3;
  width: 100%;
}

.menu {
  position: fixed;
  top: 0;
  width: 100%;
  visibility: hidden;

  &.show {
    visibility: visible;

    .menu-nav {
      // Slide in from top
      transform: translate3d(0, 0, 0);
    }

    .menu-branding {
      // Slide in from bottom
      transform: translate3d(0, 0, 0);
    }

    .nav-item {
      transform: translate3d(0, 0, 0);
    }
  }

  &-branding,
  &-nav {
    display: flex;
    flex-flow: column wrap;
    align-items: center;
    justify-content: center;
    float: left;
    width: 50%;
    height: 100vh;
    overflow: hidden;
  }

  &-nav {
    margin: 0;
    padding: 0;
    background: darken($main-color, 5);
    list-style: none;
    transform: translate3d(0, -100%, 0);
    @include easeOut;
  }

  // Branding Side
  &-branding {
    background: $main-color;
    transform: translate3d(0, 100%, 0);
    @include easeOut;
  }

  .nav-item {
    transform: translate3d(600px, 0, 0);
    @include easeOut;

    .router-link-exact-active {
      color: $accent-color;
    }
  }

  .nav-link {
    display: inline-block;
    position: relative;
    font-size: 30px;
    text-transform: uppercase;
    padding: 1rem 0;
    font-weight: 300;
    color: set-text-color($main-color);
    text-decoration: none;
    @include easeOut;

    &:hover {
      color: $accent-color;
    }
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
  .menu {
    height: 100%;
    overflow: hidden;
  }

  ul.menu-nav,
  div.menu-branding {
    float: none;
    width: 100%;
    min-height: 0;

    &.show {
      transform: translate3d(0, 0, 0);
    }
  }

  .menu-nav {
    height: calc(100% - 150px);
    transform: translate3d(-100%, 0, 0);
    font-size: 24px;
  }

  .menu-branding {
    height: 150px;
    transform: translate3d(100%, 0, 0);
  }
}

// Delay each nav item slide by 0.1s
@for $x from 1 through 4 {
  .nav-item:nth-child(#{$x}) {
    transition-delay: $x * 0.1s;
  }
}
</style>
