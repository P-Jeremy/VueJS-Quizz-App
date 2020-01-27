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
export default {
  props: {
    currentQuestion: Object,
    nextQuestion: Function
  },
  data() {
    return {
      selectedIndex: null
    }
  },
  computed: {
    answers() {
      let answers = [...this.currentQuestion.incorrect_answers]
      answers.push(this.currentQuestion.correct_answer)
      return answers
    }
  },
  methods: {
    selectAnswer(i) {
      this.selectedIndex = i
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
</style>