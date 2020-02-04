<template>
  <div class="question_box">
    <b-jumbotron>
      <template v-slot:lead>
        {{ currentQuestion.question }}
      </template>
      <hr class="my-4">
      <b-list-group>
        <b-list-group-item
        v-for="(answer, index) in shuffledAnswers" 
        :key="index"
        @click="selectAnswer(index)"
        :class="[selectedIndex === index ? 'selected': '']"
        >
        {{ answer }}
        </b-list-group-item>
      </b-list-group>
      <b-button 
        variant="primary"
        @click="submitAnswer"
      >
        Submit
      </b-button>
      <b-button @click="nextQuestion" variant="success" href="#">Next</b-button>
    </b-jumbotron>
  </div>
</template>

<script>
import shuffle from 'lodash.shuffle';
export default {
  props: {
    currentQuestion: Object,
    nextQuestion: Function,
    increment: Function
  },
  data() {
    return {
      selectedIndex: null,
      correctIndex: null,
      shuffledAnswers: [],
    }
  },
  computed: {
    answers() {
      let answers = [...this.currentQuestion.incorrect_answers]
      answers.push(this.currentQuestion.correct_answer)
      return answers
    }
  },
  watch: {
    // currentQuestion() {
    //   this.selectedIndex = null
    //   this.shuffleAnswers()
    // }
    currentQuestion: {
      immediate: true,
      handler() {
        this.selectedIndex= null
        this.shuffleAnswers()
      }
    }
  },
  methods: {
    selectAnswer(i) {
      this.selectedIndex = i
    },
    shuffleAnswers() {
      let answers = [...this.currentQuestion.incorrect_answers]
      answers.push(this.currentQuestion.correct_answer)
      this.shuffledAnswers = shuffle(answers)
      this.correctIndex = this.shuffledAnswers.indexOf(this.currentQuestion.correct_answer)
    },
    submitAnswer() {
      let isCorrect = false
      if (this.selectedIndex === this.correctIndex) {
        isCorrect = true
      }
      this.increment(isCorrect)
    }
  }
}
</script>

<style scoped>

  .list-group {
    margin: 1rem
  }

    .list-group-item:hover {
    background: #EEE;
    cursor: pointer
  }

  .btn {
    margin: 1rem
  }

  .selected {
    background-color: lightblue
  }

  .correct {
    background-color: lightgreen
  }

    .incorrect {
    background-color: lightcoral
  }

</style>