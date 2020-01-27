<template>
  <div id="app">
    <Header/>
    <b-container class="bv-example-row">
      <b-row>
        <b-col sm="8" offset="2">
          <Questions 
            v-if="questions.length"
            :currentQuestion="questions[index]"
            :nextQuestion="nextQuestion"
          />
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import Header from './components/Header.vue'
import Questions from './components/Questions.vue'

export default {
  name: 'app',
  components: {
    Header,
    Questions
  },
  data(){
    return {
      questions: [],
      index: 0
    }
  },
  methods: {
    nextQuestion() {
      this.index ++
    }
  },
  mounted: function() {
    fetch('https://opentdb.com/api.php?amount=5&category=29&difficulty=medium&type=multiple', {
      method:'get'
    })
    .then((res) => res.json())
    // eslint-disable-next-line no-console
    .then((json) => {
      this.questions = json.results
    })
  }
  
}
</script>
