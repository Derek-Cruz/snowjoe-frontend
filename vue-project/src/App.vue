
<template>
  <Header :header="header" />
  <form>
    <ol>
      <li v-for="question in questions" :key="question.question">
        {{ question.question }}
        <div v-for="c of question.choices" :key="c">
        <input type="radio" name="choice" v-model="answer" :value="c" />
        {{ c }}
      </div>
      </li>
    </ol>
    <button type="button" @click="submit">submit</button>
  </form>
  <p>score: {{ score }}</p>
</template>

<script>
import Header from "./components/Header-quiz.vue"

const questions = [
  {
    question: "What is American football called in England?",
    choices: ["American football", "football", "Handball"],
    rightAnswer: "American football",
  },
  {
    question: "What is the largest country in the world?",
    choices: ["Russia", "Canada", "United States"],
    rightAnswer: "Russia",
  },
  {
    question: "What is the 100th digit of Pi?",
    choices: [9, 4, 7],
    rightAnswer: 9,
  },
];
export default {
  components: {
    Header
  },
  data() {
    return {
      header: 'Quiz Application',
      questions,
      score: 0,
      questionIndex: 0,
      question: questions[0],
      answer: "",
    };
  },
  methods: {
    submit() {
      const { answer, question, questions, questionIndex } = this;
      if (answer === question.rightAnswer) {
        this.score++;
      }
      if (questionIndex < questions.length) {
        this.questionIndex++;
        this.question = { ...questions[this.questionIndex] };
      }
    },
  },
};
</script>

<style>

body {
  background: #f4f6f6;
  margin: 0;
}

</style>
