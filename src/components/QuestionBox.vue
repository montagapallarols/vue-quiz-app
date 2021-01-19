<template>
  <div>
    <b-jumbotron>
      <template #lead>
        <!-- Access question inside question object -->
        {{ currentQuestion.question }}
      </template>

      <hr class="my-4" />

      <b-list-group>
        <b-list-group-item
          v-for="(answer, index) in answers"
          :key="index"
          @click="selectAnswer(index)"
          :class="[selectedIndex === index ? 'selected' : '']"
        >
          <!-- Bind css class to item above -->
          {{ answer }}</b-list-group-item
        >
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
  // Save index of selected answer
  data() {
    return {
      selectedIndex: null,
    };
  },
  computed: {
    answers() {
      // Use 'this' to access a data prop
      let answers = [...this.currentQuestion.incorrect_answers];
      answers.push(this.currentQuestion.correct_answer);
      return answers;
    },
  },
  methods: {
    // On click function to get index of selected answer and save it in data
    selectAnswer(index) {
      this.selectedIndex = index;
      // console.log(index);
    },
  },
};
</script>

<!-- Use 'scoped' to apply styling only to this component -->
<style scoped>
.list-group {
  margin-bottom: 15px;
}

.list-group-item:hover {
  background-color: #eff7e1;
  cursor: pointer;
}

.btn {
  margin: 0 5px;
}

.selected {
  background-color: #55b3b1;
}

.correct {
  background-color: lightgreen;
}

.incorrect {
  background-color: red;
}
</style>
