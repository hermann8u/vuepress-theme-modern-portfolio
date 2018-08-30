<template>
  <div id="home">
    <Header/>
    <Socials/>
  </div>
</template>

<script>
import Header from './Header.vue'
import Socials from './Socials.vue'

export default {
  components: { Header, Socials }
}
</script>

<style scopped lang="scss">
@import '../scss/config';
@import '../scss/mixins';

#home {
  overflow: hidden;
  h1 {
    margin-top: 20vh;
  }
}

// Smartphones
@include mediaSm {
  #home h1 {
    margin-top: 10vh;
  }
}
</style>