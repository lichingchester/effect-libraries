<template>
  <div class="background">
    <svg ref="svg" xmlns="http://www.w3.org/2000/svg">
      <circle cx="200" cy="200" r="20" fill="blue" class="dot" />
    </svg>
  </div>
</template>

<script>
import { TweenMax, Power4 } from 'gsap';

export default {
  mounted() {
    const svg = this.$refs.svg;

    TweenMax.to(svg.querySelector('.dot'), 1.5, {
      scale: 0,
      transformOrigin: 'center',
      repeat: 2,
      yoyo: true,
      ease: Power4.easeInOut
    });
  }
};
</script>

<style lang="scss" scoped>
svg {
  width: 100%;
  height: 100%;
}

.background {
  position: fixed;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
}
</style>
