<template>
  <div>
    <EfCursor />
    <RafSample />
  </div>
</template>

<script>
import EfCursor from '@/components/Cursor.vue';
import RafSample from '@/components/RafSample.vue';

export default {
  components: {
    EfCursor,
    RafSample
  }
};
</script>

<style lang="scss" scoped>
*,
*:before,
*:after {
  box-sizing: border-box;
  margin: 0;
  cursor: none;
}

body {
  background-color: #000;
}
</style>
