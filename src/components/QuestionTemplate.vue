<template>
  <div>
    <div v-for="(question, index) in questions" :key="question.id">
      <p>{{ question.question }}</p>
      <div v-for="(answer, answerIndex) in question.answers" :key="answerIndex">
        <input type="radio" :id="'answer-' + index + '-' + answerIndex" :name="'answer-' + index" :value="answer.answer"
          v-model="selected[index]">
        <label :for="'answer-' + index + '-' + answerIndex">{{ answer.answer }}</label>
      </div>
    </div>
    <button type="submit" @click.prevent="submitQuiz">Submit Answers</button>
  </div>

  <modal-score v-if="sentScore" :score="this.totalScore()" :callback="toggleModal" />
</template>

<script>
import axios from 'axios'
import ModalScore from './ModalScore.vue'

export default {
  props: {
    questions: {
      type: Array,
      required: true,
    },
  },
  components: {
    ModalScore,
  },
  data() {
    return {
      selected: [],
      sentScore: false,
    }
  },
  methods: {
    submitQuiz() {
      this.toggleModal()
      this.sendScore()
    },
    totalScore() {
      let total = 0
      this.selected.forEach((answer, index) => {
        const question = this.questions[index]
        if (answer === this.getCorrectVal(question.answers)) {
          total++
        }
      })
      return total
    },
    getCorrectVal(answers) {
      return answers.find((answer) => answer.correct).answer
    },
    toggleModal() {
      this.sentScore = !this.sentScore
    },
    async sendScore() {
      try {
        await axios.post('http://localhost:3001/records', {
          grade: this.totalScore(),
          first_name: '',
          last_name: '',
        })
      } catch (error) {
        console.error(error)
      }
    },
  },
}
</script>
