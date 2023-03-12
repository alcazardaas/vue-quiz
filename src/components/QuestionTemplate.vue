<template>
  <div>
    <div v-for="(question, index) in questions" :key="question.id">
      <p>{{ question.question }}</p>
      <div v-for="(answer, answerIndex) in question.answers" :key="answerIndex">
        <input type="radio" :id="'answer-' + index + '-' + answerIndex" :name="'answer-' + index" :value="answerIndex"
          v-model="selected[index]">
        <label :for="'answer-' + index + '-' + answerIndex">{{ answer.answer }}</label>
      </div>
    </div>
    <button @click="submitAnswers">Submit Answers</button>
  </div>
</template>

<script>
export default {
  props: {
    questions: {
      type: Array,
      required: true,
    },
  },
  data() {
    return {
      selected: [],
    };
  },
  methods: {
    submitAnswers() {
      // do something with the selected answers
    },
  },
};
</script>


<style></style>