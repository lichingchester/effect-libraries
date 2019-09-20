<template>
  <div ref="raf" class="raf-test"></div>
</template>

<script>
import { TweenLite } from 'gsap';

export default {
  data() {
    return {
      frameId: null,

      isMove: false,
      efProps: {
        left: 0,
        endLeft: 0
      }
    };
  },
  mounted() {
    this.initEvents();
    this.initStatus();
  },
  methods: {
    initEvents() {
      if (process.client) {
        this.$refs.raf.addEventListener('click', () => {
          // init status
          this.initStatus();

          // start
          this.start();
          TweenLite.to(this.efProps, 2, { left: this.efProps.endLeft });

          this.isMove = true;

          console.log('click', this.isMove);
        });
      }
    },

    initStatus() {
      if (process.client) {
        this.efProps.left = 0;
        this.efProps.endLeft = window.innerWidth - 100;
      }
    },

    start() {
      if (this.frameId) {
        this.stop();
      }

      this.frameId = requestAnimationFrame(() => this.render());
    },

    stop() {
      cancelAnimationFrame(this.frameId);
    },

    render() {
      if (this.efProps.left >= this.efProps.endLeft) {
        this.stop();
        return;
      }

      console.log('requestAnimationFrame', this.efProps.left);

      this.$refs.raf.style.left = `${this.efProps.left}px`;
      this.frameId = requestAnimationFrame(() => this.render());
    }
  }
};
</script>

<style lang="scss" scoped>
.raf-test {
  position: fixed;
  left: 0%;
  right: 50%;
  width: 100px;
  height: 100px;
  background: red;
}
</style>
