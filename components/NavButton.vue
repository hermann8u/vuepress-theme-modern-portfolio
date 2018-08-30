<template>
  <div class="menu-btn" :class="{close: isNavOpen}">
    <div class="btn-line"></div>
    <div class="btn-line"></div>
    <div class="btn-line"></div>
  </div>
</template>

<script>

export default {
  props: {
    isNavOpen: Boolean
  }
}
</script>

<style scopped lang="scss">
@import '../scss/config';
@import '../scss/mixins';

.menu-btn {
  background: darken($main-color, 5);
  padding: 10px 10px 5px;
  border-radius: 5px;
  position: absolute;
  z-index: 3;
  right: 20px;
  top: 20px;
  // border: 1px solid $accent-color;
  cursor: pointer;
  @include easeOut;

  .btn-line {
    width: 28px;
    height: 3px;
    margin: 0 0 5px 0;
    background: set-text-color($main-color);
    @include easeOut;
  }

  &.close {
    transform: rotate(180deg);
    .btn-line {
      // Line 1 - Rotate
      &:nth-child(1) {
        transform: rotate(45deg) translate(5px, 5px);
      }
      // Line 2 - Hide
      &:nth-child(2) {
        opacity: 0;
      }
      // Line 3 - Rotate
      &:nth-child(3) {
        transform: rotate(-45deg) translate(7px, -6px);
      }
    }
  }
}
</style>