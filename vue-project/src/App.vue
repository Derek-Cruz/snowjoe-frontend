<template>
  <Header :header="header" />
  <div class="container">
    <h1 class="h1-placement">Quiz 1 - Snow Joe</h1>
    <div v-if="showResults" class="results-placement">
      <h3 class="results-style">Results</h3>
      <p class="score-style">You got {{ score }} / 3 questions correct</p>
      <p class="percent-style" :class="`${ (100 * score / 3).toFixed(2) <= 50 ? 'red' : 'green' }`">{{ (100 * score / 3).toFixed(2) }} %</p>
    </div>
    <form @submit.prevent="onSubmit">
      <ul>
        <li
          v-for="(q, questionIndex) of questions"
          :key="q.id"
          :class="`li-style ${isError[questionIndex] ? 'highlight' : ''} ${isCorrect[questionIndex] ? 'correct' : ''} ${isWrong[questionIndex] ? 'wrong' : ''}`"
        >
          <p class="p-style">
            {{ questionIndex + 1 }}. {{ q.question }}
          </p>
          <div class="div-placement">
            <div :for="q.id" v-for="(c, choiceIndex) of q.answers" :key="c" :class="`div-style ${q.correctAnswer === choiceIndex && showResults && q.correctAnswer !== userChoices[questionIndex] ? 'green-background' : ''}`">
              <input type="radio" :name="q.id" :value="userChoices[questionIndex]" @change="updateChoice(questionIndex, choiceIndex)" />
              {{ c }}
            </div>
          </div>
          <div v-if="showResults">
            <p :class="`p-correct-wrong ${isCorrect[questionIndex] ? 'green' : 'red'}`">{{ isCorrect[questionIndex] ? 'Correct' : 'Wrong' }}</p>
          </div>
        </li>
      </ul>
      <div class="submit-placement">
        <input type="submit" class="button-style" />
      </div>
    </form>
    <div v-if="showWarning" class="warning-placement">
      <p class="warning-style">Answer ask questions before submitting. Unanswered questions are displayed in yellow.</p>
    </div>
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
      isError: [],
      isCorrect: [],
      isWrong: [],
      showResults: false,
      showWarning: false,
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
      for (let i = 0; i < this.userChoices.length; i++) {
        if (this.userChoices[i] === null) {
          this.isError[i] = true
          this.showWarning = true
        }
      }
      const isFalse = (currentValue) => currentValue === false;
      if (this.isError.every(isFalse)) {
        for (let i = 0; i < this.userChoices.length; i++) {
          if (this.userChoices[i] === this.questions[i].correctAnswer) {
              this.isCorrect[i] = true
              this.score++
            } else if (this.userChoices[i] !== this.questions[i].correctAnswer) {
              this.isWrong[i] = true
            }
         }
         this.showResults = true
       }
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
  padding: 0 1.25rem;
}

.container {
  margin-top: 3.75rem;
}

.score-style {
  font-size: 1.3rem;
  margin: 0.813rem 0 0;
}

.percent-style {
  font-size: 1.3rem;
  margin: 0.375rem 0 0;
}

.red {
  color: red;
}

.green {
  color: green;
}

.green-background {
  width: 65%;
  height: 30px;
  background-color: #24a824;
  line-height: 31px;
  border-radius: 8px;
  border: black solid 1px;
}

.results-style {
  font-weight: 500;
  font-size: 1.8rem;
  margin: 0;
  text-decoration: underline;
}

.results-placement {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.submit-placement {
  display: flex;
  justify-content: center;
}

.warning-placement {
  display: flex;
  justify-content: center;
}

.h1-placement {
  padding-left: 20px;
  font-size: 1.7rem;
  font-weight: 500;
 }

.li-style {
  box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
  width: 100%;
  border-radius: 5px;
  background: white;
  margin-bottom: 30px;
  list-style-type: none;
  padding: 1.25rem 0 0.625rem 0;
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

.warning-style {
  display: flex;
  width: 70%;
  color: red;
  justify-content: center;
}

.button-style {
  background-color: green;
  border: black solid 1px;
  color: white;
  padding: 0.625rem 0.938rem;
  text-decoration: none;
  margin: 0.25rem 0.125rem;
  cursor: pointer;
  border-radius: 5px;
}

.p-style {
  padding: 0 1.563rem;
  margin-top: 0;
  margin-bottom: 0.813rem;
  font-size: 1.2rem;
}

.p-correct-wrong {
  display: flex;
  margin: 0 0.625rem 0 0;
  justify-content: flex-end;
}

.div-placement {
  padding: 0 2.563rem;
  margin-bottom: 0.625rem;
  font-size: 1rem;
}

.div-style {
  margin-bottom: 0.75rem;
}

@media only screen and (min-width: 768px) {
  .container {
    max-width: 900px;
    margin: 4.063rem auto 0;
  }

  .warning-style {
    width: unset;
  }
}
</style>
