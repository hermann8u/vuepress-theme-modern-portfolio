<template>
  <i class="fa" aria-hidden="true" :class="faClass"></i>
</template>

<script>
export default {
  props: {
    icon: {
      type: String,
      required: true
    }
  },
  computed: {
    faClass () {
      return 'fa-' + this.icon;
    }
  }
}
</script>

<style lang="scss" scoped>
  $fa-font-path: "~font-awesome/fonts";
  @import "~font-awesome/scss/font-awesome";
</style>

