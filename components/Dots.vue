<template>
  <svg
    ref="svg"
    xmlns="http://www.w3.org/2000/svg"
    xmlns:xlink="http://www.w3.org/1999/xlink"
  ></svg>
</template>

<script>
export default {
  mounted() {
    // initial
    const dotSpacing = 20;

    console.log(dotSpacing);

    // const namespace = 'http://www.w3.org/2000/svg';

    // let x = 0;
    // let y = 0;
    // let isKeepDraw = true;
    // let isEndWidth = false;
    // let isEndHeight = false;

    // while (isKeepDraw) {
    //   while (!isEndWidth) {
    //     console.log('x', x, 'y', y);

    //     const circle = document.createElementNS(namespace, 'circle');
    //     circle.setAttribute('cx', x);
    //     circle.setAttribute('cy', y);
    //     circle.setAttribute('r', 5);
    //     this.$refs.svg.appendChild(circle);

    //     x += dotSpacing;

    //     if (x >= 1920) {
    //       isEndWidth = true;
    //     }
    //   }
    //   x = 0;
    //   y += dotSpacing;

    //   if (y >= 920) {
    //     isEndHeight = true;
    //   } else {
    //     isEndWidth = false;
    //   }

    //   if (isEndHeight && isEndWidth) {
    //     isKeepDraw = false;
    //   }
    // }
  }
};
</script>

<style lang="scss" scoped>
svg {
  position: absolute;
  width: 1920px;
  height: 100%;
  left: 50%;
  transform: translateX(-50%);
}
</style>
