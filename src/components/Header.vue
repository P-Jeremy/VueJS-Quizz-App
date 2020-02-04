<template>
  <div>
    <b-nav tabs>
      <b-nav-item disabled>Quizz app</b-nav-item>
      <b-nav-item disabled>Counter: {{correctCounter}}/{{totalAnswers}}</b-nav-item>
    </b-nav>
  </div>
</template>

<script>
export default {
  props: [
    'totalAnswers',
    'correctCounter'
  ]
}
</script>