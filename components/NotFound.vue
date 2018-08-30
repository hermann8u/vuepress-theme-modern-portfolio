<template>
  <div id="home">
    <h1 class="lg-header">404</h1>
    <h2 class="sm-header">{{ getMsg }}</h2>
    <<router-link to="/"Take me home></router-link>
  </div>
</template>

<script>
const msgs = [
  `There's nothing here.`,
  `How did we get here?`,
  `That's a Four-Oh-Four.`,
  `Looks like we've got some broken links.`
]
export default {
  methods: {
    getMsg () {
      return msgs[Math.floor(Math.random() * msgs.length)]
    }
  }
}
</script>

<style scopped lang="scss">
  #home {
    overflow: hidden;
    h1 {
      margin-top: 20vh;
    }
  }
</style>