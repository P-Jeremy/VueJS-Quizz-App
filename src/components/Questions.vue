<template>
  <div class="question_box">
    <b-jumbotron>
      <template v-slot:lead>
        {{ currentQuestion.question }}
      </template>
      <hr class="my-4">
      <b-list-group>
        <b-list-group-item
        v-for="(answer, index) in answers" 
        :key="index"
        @click="selectAnswer(index)"
        :class="[selectedIndex === index ? 'selected': '']"
        >
        {{ answer }}
        </b-list-group-item>
      </b-list-group>
      <b-button variant="primary" >Submit</b-button>
      <b-button @click="nextQuestion" variant="success" href="#">Next</b-button>
    </b-jumbotron>
  </div>
</template>

<script>
import shuffle from 'lodash.shuffle';
export default {
  props: {
    currentQuestion: Object,
    nextQuestion: Function
  },
  data() {
    return {
      selectedIndex: null,
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
    currentQuestion() {
      this.selectedIndex = null
      this.shuffleAnswers()
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
      // eslint-disable-next-line no-console
      console.log("SHUFFLE", this.shuffledAnswers);
      
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