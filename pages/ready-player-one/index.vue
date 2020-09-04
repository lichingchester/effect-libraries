<template>
  <div ref="wrapper" class="ready-player-one hover">
    <div class="main" @mouseenter="mouseenter" @mouseleave="mouseleave">
      <img src="/ready-player-one/logo.png" alt="" class="logo" />
      <img src="/ready-player-one/actor.png" alt="" class="actor" />

      <div class="enter-text">
        <span>PRESS</span>
        <span>START</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  methods: {
    mouseenter() {
      // this.$refs.wrapper.classList.add('hover');
    },
    mouseleave() {
      // this.$refs.wrapper.classList.remove('hover');
    }
  }
};
</script>

<style lang="scss" scoped>
@font-face {
  font-family: 'Ready-Player-One';
  src: url('/ready-player-one/Ready-Player-One.otf');
}

.ready-player-one {
  position: fixed;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  background-image: url('/ready-player-one/back-background.jpg');
  background-position: center;
  background-size: cover;
  background-repeat: no-repeat;
  font-family: 'Ready-Player-One';

  .main {
    position: absolute;
    left: 50%;
    top: 50%;
    width: 1252px;
    height: 704px;
    transform: translate(-50%, -50%);
    background-image: url('/ready-player-one/front-background.jpg');
    background-position: center;
    background-size: cover;
    background-repeat: no-repeat;
    border-radius: 20px;
    box-shadow: 20px 20px 30px 0 rgba(0, 0, 0, 0.16);
  }

  .logo {
    position: absolute;
    left: 50%;
    width: 988px;
    height: auto;
    transform-origin: top center;
    filter: blur(5px);
    opacity: 0.5;
    top: 3rem;
    transform: translateX(-50%);
    transition: 1s cubic-bezier(0.25, 1, 0.5, 1);
  }
  &.hover {
    .logo {
      width: 130px;
      top: 1.5rem;
      opacity: 1;
      transform: translateX(-50%);
      filter: blur(0);
    }
  }

  .actor {
    position: absolute;
    left: 50%;
    bottom: 0;
    height: 600px;
    transform: translateX(-50%);
  }

  .enter-text {
    position: absolute;
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%);
    font-size: 93px;
    white-space: nowrap;
    color: white;
    // animation: flicker 1.5s infinite alternate;

    span:first-child {
      margin-right: 320px;
      margin-left: 10px;
    }
  }
}

/* Animate neon flicker */
// @keyframes flicker {
//   0%,
//   19%,
//   21%,
//   23%,
//   25%,
//   54%,
//   56%,
//   100% {
//     text-shadow: -0.2rem -0.2rem 1rem #fff, 0.2rem 0.2rem 1rem #fff,
//       0 0 1rem #fff, 0 0 2rem #fff, 0 0 3rem #fff, 0 0 4rem #fff, 0 0 5rem #fff;
//   }

//   20%,
//   24%,
//   55% {
//     text-shadow: none;
//     box-shadow: none;
//   }
// }
</style>
