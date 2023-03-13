<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <!-- <parallax-background /> -->
  <form-questions/>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import FormQuestions from './components/FormQuestions.vue';
import ParallaxBackground from './components/ParallaxBackground.vue';

export default defineComponent({
  name: 'App',
  components: {
    FormQuestions,
    // ParallaxBackground
  }
});
</script>

<style lang="less">
html {
  background: #ccc;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #0012FF;
  margin: 4em 1em 0em 1em;
}
</style>
