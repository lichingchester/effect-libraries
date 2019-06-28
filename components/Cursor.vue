<template>
  <div ref="cursor" class="cursor">
    <div class="cursor__inner cursor__inner--circle"></div>
    <div class="cursor__inner cursor__inner--dot"></div>
  </div>
</template>

<script>
export default {
  name: 'EfCursor',
  data() {
    return {
      DOM: {
        el: null,
        dot: null,
        circle: null
      },
      bounds: null,
      scale: null,
      opacity: null,
      mousePos: null,
      lastMousePos: null,
      lastScale: null
    };
  },
  computed: {
    body() {
      if (process.client) {
        return document.body;
      } else {
        return null;
      }
    }
  },
  mounted() {
    this.init();
  },
  methods: {
    lerp(a, b, n) {
      return (1 - n) * a + n * b;
    },

    getMousePos(e) {
      let posx = 0;
      let posy = 0;
      if (!e) e = window.event;
      if (e.pageX || e.pageY) {
        posx = e.pageX;
        posy = e.pageY;
      } else if (e.clientX || e.clientY) {
        posx =
          e.clientX +
          this.body.scrollLeft +
          document.documentElement.scrollLeft;
        posy =
          e.clientY + this.body.scrollTop + document.documentElement.scrollTop;
      }
      return { x: posx, y: posy };
    },

    init() {
      if (process.client) {
        this.constructor(this.$refs.cursor);
      }
    },

    /**
     * Class Cursor
     */
    constructor(el) {
      this.DOM = { el: el };
      this.DOM.dot = this.DOM.el.querySelector('.cursor__inner--dot');
      this.DOM.circle = this.DOM.el.querySelector('.cursor__inner--circle');
      this.bounds = {
        dot: this.DOM.dot.getBoundingClientRect(),
        circle: this.DOM.circle.getBoundingClientRect()
      };
      this.scale = 1;
      this.opacity = 1;
      this.mousePos = { x: 0, y: 0 };
      this.lastMousePos = { dot: { x: 0, y: 0 }, circle: { x: 0, y: 0 } };
      this.lastScale = 1;

      this.initEvents();
      requestAnimationFrame(() => this.render());
    },

    initEvents() {
      window.addEventListener(
        'mousemove',
        ev => (this.mousePos = this.getMousePos(ev))
      );
    },

    render() {
      this.lastMousePos.dot.x = this.lerp(
        this.lastMousePos.dot.x,
        this.mousePos.x - this.bounds.dot.width / 2,
        1
      );
      this.lastMousePos.dot.y = this.lerp(
        this.lastMousePos.dot.y,
        this.mousePos.y - this.bounds.dot.height / 2,
        1
      );
      this.lastMousePos.circle.x = this.lerp(
        this.lastMousePos.circle.x,
        this.mousePos.x - this.bounds.circle.width / 2,
        0.15
      );
      this.lastMousePos.circle.y = this.lerp(
        this.lastMousePos.circle.y,
        this.mousePos.y - this.bounds.circle.height / 2,
        0.15
      );
      this.lastScale = this.lerp(this.lastScale, this.scale, 0.15);
      this.DOM.dot.style.transform = `translateX(${
        this.lastMousePos.dot.x
      }px) translateY(${this.lastMousePos.dot.y}px)`;
      this.DOM.circle.style.transform = `translateX(${
        this.lastMousePos.circle.x
      }px) translateY(${this.lastMousePos.circle.y}px) scale(${
        this.lastScale
      })`;
      requestAnimationFrame(() => this.render());
    },

    enter() {
      this.scale = 1.5;
      this.DOM.dot.style.display = 'none';
    },

    leave() {
      this.scale = 1;
      this.DOM.dot.style.display = '';
    }
  }
};
</script>

<style lang="scss" scoped>
.cursor {
  position: fixed;
  display: block;
  left: 0;
  top: 0;
  height: 100%;
  width: 100%;
  mix-blend-mode: difference;
  pointer-events: none;
  z-index: 9999;
}

body.mobile .cursor {
  display: none;
}

.cursor__inner {
  z-index: 9999;
  pointer-events: none;
  position: absolute;
  top: 0;
  left: 0;
  border-radius: 50%;
}

.cursor__inner--dot {
  width: 8px;
  height: 8px;
  background: #fff;
}

.cursor__inner--circle {
  width: 40px;
  height: 40px;
  border: 1px solid #fff;
}
</style>
