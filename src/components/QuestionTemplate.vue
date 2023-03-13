<template>
  <div>
    <div class="question-container" v-for="(question, index) in questions" :key="question.id">
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

<style lang="less">
.question-container {
  background: white;
  border-radius: 5px;
  padding: 1em;
  margin: 1em 0;

  div {
    display: flex;
    padding-left: 24%;

    @media screen and (min-width: 768px) {
      padding-left: 40%;
    }

    input[type="radio"] {
      appearance: none;
      border: 2px solid #ccc;
      border-radius: 50%;
      width: 1.2em;
      height: 1.2em;
      margin-right: 0.5em;
      transition: all 0.2s ease-in-out;
    }

    label {
      font-weight: bold;
      cursor: pointer;
    }

    input[type="radio"]:checked {
      border-color: #0077cc;
      background-color: #0077cc;
    }

    input[type="radio"]:checked+label {
      color: #0092FF;
    }
  }
}

button[type="submit"] {
  background-color: #0092FF;
  margin: 2em 0;
  color: #fff;
  padding: 10px 20px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 16px;
  font-weight: bold;
}
</style>