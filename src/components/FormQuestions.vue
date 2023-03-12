<template>
  <div>
    <question-template :questions="questions" />
  </div>
</template>

<script>
import axios from 'axios';
import QuestionTemplate from './QuestionTemplate.vue';

export default {
  components: {
    QuestionTemplate,
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
