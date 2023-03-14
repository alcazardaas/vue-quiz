<template>
  <div class="wrapper">
    <header>
      <img src="./assets/waves.svg" class="background">
      <img src="./assets/bubble.svg" class="foreground">
      <h1 class="title">
        {{ title }}
      </h1>
    </header>
    <form-questions />
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import FormQuestions from './components/FormQuestions.vue';

export default defineComponent({
  name: 'App',
  components: {
    FormQuestions,
  },
  data() {
    return {
      title: 'Quiz App',
    };
  },
});
</script>

<style lang="less">
body {
  margin: 0;
}

html {
  background: #ccc;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #0012FF;

  .wrapper {
    height: 100vh;
    overflow-y: auto;
    overflow-x: hidden;
    perspective: 10px;

    header {
      position: relative;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100%;
      transform-style: preserve-3d;
      z-index: -1;

      .background,
      .foreground {
        position: absolute;
        width: 100%;
        height: 100%;
        object-fit: cover;
        z-index: -1;
      }

      .background {
        transform: translateZ(-10px) scale(2);
      }

      .foreground {
        width: 100%;
        transform: translateZ(-5px) scale(1.5);

        @media screen and (min-width: 1200px) {
          width: 67%;
        }
      }
    }

    .title {
      font-size: 7rem;
      color: #fff;
      text-shadow: 0 0 5px #000;
    }
  }
}
</style>
