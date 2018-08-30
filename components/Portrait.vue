<template>
  <div class="portrait" :style="{ 'background-image': 'url(' + portrait + ')' }" ></div>
</template>

<script>
export default {
  computed: {
    portrait () {
      return this.$site.themeConfig.portrait;
    }
  }
}
</script>

<style scopped lang="scss">
@import '../scss/config';
@import '../scss/mixins';

.portrait {
  width: 250px;
  height: 250px;
  border-radius: 50%;
  border: solid 3px $accent-color;
  background-repeat: no-repeat;
  background-size: 100% 100%;
}

@include mediaMd {
  .portrait {
    width: 125px;
    height: 125px;
  }
}
</style>