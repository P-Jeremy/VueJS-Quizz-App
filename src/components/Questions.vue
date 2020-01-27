<template>
  <div class="question_box">
    <b-jumbotron>
      <template v-slot:lead>
        {{ currentQuestion.question }}
      </template>
      <hr class="my-4">
      <p>
        answers
      </p>
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
  }
}
</script>