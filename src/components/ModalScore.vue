<template>
  <div class="modal" @click.self="closeModal">
    <div class="score" @click.stop>
      <loader-component v-if="generalGrades.length === 0" />
      <div v-else>
        <h3>Your total score is <b>{{ score }}</b></h3>
        <h4>You were better than <b>{{ this.getGradeComparisonBetterThan() }}</b> of all quizers</h4>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import LoaderComponent from './LoaderComponent.vue'

export default {
  components: {
    LoaderComponent
  },
  props: {
    score: {
      type: Number,
      required: true,
    },
    callback: {
      type: Function,
      required: true
    }
  },
  data() {
    return {
      generalGrades: [],
    }
  },
  methods: {
    closeModal() {
      this.callback()
    },
    getGradeComparisonBetterThan() {
      const total = this.generalGrades.length
      const betterThan = this.generalGrades.filter(grade => grade.grade < this.score).length
      return Math.round((betterThan / total) * 100)+'%'
    },
  },
  async created() {
    try {
      const response = await axios.get('http://localhost:3001/records');
      this.generalGrades = response.data;
    } catch (error) {
      console.error(error);
    }
  }
}
</script>

<style lang="less">
.modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  z-index: 9999;
  display: flex;
  justify-content: center;
  align-items: center;

  &::before {
    content: "";
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(255, 255, 255, 0.2);
    z-index: -1;
  }

  .score {
    background-color: #ccc;
    border-radius: 5px;
    padding: 20px;
    font-size: 36px;
    text-align: center;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.3);
    margin: 1em;
  }
}
</style>