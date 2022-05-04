
<template>
  <Header :header="header" />
  <h1>Quiz 1 - HTML/CSS/JS Practice</h1>
  <form>
    <ul>
      <li v-for="(question, index) in questions" :key="question.question" class="testing-li">
        <p class="testing-p">
          {{ index }}. {{ question.question }}
        </p>
        <div v-for="c of question.choices" :key="c" class="testing-div">
        <input type="radio" name="choice" v-model="answer" :value="c" />
        {{ c }}
      </div>
      </li>
    </ul>
  </form>
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
      answer: "",
    };
  },
};
</script>

<style>
body {
  background: #f4f6f6;
  margin: 0;
}

 ul {
   padding: 0 20px;
 }

.testing-li {
  box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
  width: 100%;
  border-radius: 5px;
  background: white;
  margin-bottom: 30px;
  list-style-type: none;
  padding: 20px 0;
}

.testing-p {
  padding: 0px 25px;
      margin-top: 0;
  margin-bottom: 13px;
  font-size: 1.2rem;
}

.testing-div {
  padding: 0px 21px;
  margin-bottom: 10px;
  font-size: 1rem;
}
</style>
