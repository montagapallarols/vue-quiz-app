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

      <b-button variant="primary" @click="submitAnswer">
        Submit
      </b-button>
      <b-button @click="next" variant="success" href="#">Next</b-button>
    </b-jumbotron>
  </div>
</template>

<!-- We have to reference the props here in order for the props data to be displayed -->
<script>
import _ from "lodash";

export default {
  props: {
    currentQuestion: Object,
    next: Function,
    increment: Function,
  },
  // Save index of selected answer
  data() {
    return {
      selectedIndex: null,
      shuffledAnswers: [],
    };
  },
  computed: {
    answers() {
      // Use 'this' to access a data prop
      let answers = [...this.currentQuestion.incorrect_answers];
      answers.push(this.currentQuestion.correct_answer);
      // We join correct answers with incorrect answer inside same array
      return answers;
    },
  },
  // It also takes an object of functions like computed/methods, but here we can watch for changes
  watch: {
    currentQuestion() {
      // Every timet the question changes, we set the index back to null & shuffle the answers
      this.selectedIndex = null;
      this.shuffleAnswers();
    },
  },
  methods: {
    // On click function to get index of selected answer and save it in data
    selectAnswer(index) {
      this.selectedIndex = index;
      // console.log(index);
    },
    submitAnswer() {
      let isCorrect = false;

      if (this.selectedIndex === this.correctIndex) {
        isCorrect = true;
      }

      // We need to pass the correct answer as prop so we can update the counter in header
      this.increment(isCorrect);
    },
    shuffleAnswers() {
      let answers = [
        ...this.currentQuestion.incorrect_answers,
        this.currentQuestion.correct_answer,
      ];
      // use shuffle method from lodash, tell it which array we want to shuffle
      this.shuffledAnswers = _.shuffle(answers);
    },
  },
  mounted() {
    // To shuffle the answers for the first question when component mounts
    // After that the answers will be shuffled every time the question changes
    this.shuffleAnswers();
  },
};
</script>

<!-- Use 'scoped' to apply styling only to this component -->
<style scoped>
.list-group {
  margin-bottom: 15px;
}

.list-group-item:hover {
  background-color: lightgrey;
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
