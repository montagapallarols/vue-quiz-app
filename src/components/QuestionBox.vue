<template>
  <div>
    <b-jumbotron>
      <template #lead>
        <!-- Access question inside question object -->
        {{ currentQuestion.question }}
      </template>

      <hr class="my-4" />

      <p>
        List of answers
      </p>

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
};
</script>
