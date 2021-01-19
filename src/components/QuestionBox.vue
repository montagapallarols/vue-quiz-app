<template>
  <div>
    <b-jumbotron>
      <template #lead>
        <!-- Access question inside question object -->
        {{ currentQuestion.question }}
      </template>

      <hr class="my-4" />

      <b-list-group>
        <b-list-group-item v-for="(answer, index) in answers" :key="index">{{
          answer
        }}</b-list-group-item>
      </b-list-group>

      <b-button variant="primary" href="#">Submit</b-button>
      <b-button @click="next" variant="success" href="#">Next</b-button>
    </b-jumbotron>
  </div>
</template>

<!-- We have to reference the props here in order for the props data to be displayed -->
<script>
export default {
  props: {
    currentQuestion: Object,
    next: Function,
  },
  computed: {
    answers() {
      // Use 'this' to access a data prop
      let answers = [...this.currentQuestion.incorrect_answers];
      answers.push(this.currentQuestion.correct_answer);
      return answers;
    },
  },
};
</script>

<!-- Use 'scoped' to apply styling only to this component -->
<style scoped>
.list-group {
  margin-bottom: 15px;
}

.btn {
  margin: 0 5px;
}
</style>
