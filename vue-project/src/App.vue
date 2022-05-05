<template>
  <Header :header="header" />
  <div class="container">
    <h1 class="testing-h1">Quiz 1 - Snow Joe</h1>

    <div v-if="showResults">
      Results: 0/100
    </div>

    <form @submit.prevent="onSubmit">
      <ul>
        <li
          v-for="(q, questionIndex) of questions"
          :key="q.id"
          :class="`testing-li ${isError[questionIndex] ? 'highlight' : ''} ${isCorrect[questionIndex] ? 'correct' : ''} ${isWrong[questionIndex] ? 'wrong' : ''}`"
        >

          <p class="testing-p">
            {{ questionIndex + 1 }}. {{ q.question }}
          </p>

          <!-- For loop for the choices for the question -->
          <div :for="q.id" v-for="(c, choiceIndex) of q.answers" :key="c" class="testing-div">
            <!-- Make sure `name` is the same as `for` in the label above-->
            <input type="radio" :name="q.id" :value="userChoices[questionIndex]" @change="updateChoice(questionIndex, choiceIndex)" />

            {{ c }}
          </div>
        </li>
      </ul>

      <div>
        <input type="submit" />
      </div>
    </form>
  </div>
</template>

<script>
import Header from "./components/Header-quiz.vue"

export default {
  components: {
    Header
  },
  data() {
    return {
      header: 'Quiz Application',
      questions: [],
      userChoices: [],
      score: 0,
      answer: "",
      isError: [],
      isCorrect: [],
      isWrong: [],
      showResults: false,
    };
  },
  mounted() {
    fetch('http://localhost:3001/questions')
    .then(res => res.json())
    .then(data => {
      this.questions = data;

      this.userChoices = Array.from(this.questions).fill(null);
      this.isError = Array.from(this.questions).fill(false);
      this.isCorrect = Array.from(this.questions).fill(false);
      this.isWrong = Array.from(this.questions).fill(false);
    })
  },
  methods: {
    updateChoice(questionIndex, choiceIndex) {
      this.userChoices[questionIndex] = choiceIndex
    },

    onSubmit() {
      // Loop 1
      // For each userChoice, check if it's null
      // if it is, then highlight it YELLOW at that index

      // Loop 2
      // For each userChoice, check if it's right or wrong
      // if it is right, then highlight it GREEN at that index
      // else, highlight it RED at the index

      // showResults = true
    }
  }
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

 .container {
  margin-top: 60px;
 }

 .testing-h1 {
   padding-left: 20px;
  font-size: 1.7rem;
  font-weight: 500;
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

.highlight {
  border: solid yellow 2px;
}

.correct {
  border: solid green 2px;
}

.wrong {
  border: solid red 2px;
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

@media only screen and (min-width: 768px) {
  .container {
    margin-top: 65px;
    max-width: 900px;
    margin: 0 auto;
  }
}
</style>
