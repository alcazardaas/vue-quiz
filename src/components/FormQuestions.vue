<template>
  <div>
    <loader-component v-if="questions.length === 0" :isCentered='true'/>
    <form v-else>
      <question-template :questions="questions" />
    </form>
  </div>
</template>

<script>
import axios from 'axios';
import QuestionTemplate from './QuestionTemplate.vue';
import LoaderComponent from './LoaderComponent.vue'

export default {
  components: {
    QuestionTemplate,
    LoaderComponent
  },
  data() {
    return {
      questions: [],
    };
  },
  async created() {
    try {
      const response = await axios.get('http://localhost:3001/questions');
      this.questions = response.data;
    } catch (error) {
      console.error(error);
    }
  },
};
</script>
