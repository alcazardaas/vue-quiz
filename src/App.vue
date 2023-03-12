<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <form-questions/>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import FormQuestions from './components/FormQuestions.vue';

export default defineComponent({
  name: 'App',
  components: {
    FormQuestions
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
  color: #2c3e50;
  margin-top: 60px;
}
</style>
