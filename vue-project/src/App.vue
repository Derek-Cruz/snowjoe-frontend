<template>
  <Header :header="header" />
  <div class="container">
    <h1 class="testing-h1">Quiz 1 - Snow Joe</h1>

    <form>
      <ul>
        <li v-for="(question, index) in questions" :key="question.question" class="testing-li ">
          <p class="testing-p">
            {{ index + 1 }}. {{ question.question }}
          </p>

          <div v-for="(value, key) in question.answers" :key="key" class="testing-div">

            <input type="radio" name="choice" v-model="userChoices[index]" />

            {{ value }}

          </div>
        </li>
      </ul>
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
    };
  },
  mounted() {
    fetch('http://localhost:3001/questions')
    .then(res => res.json())
    .then(data => {
      this.questions = data;
      this.userChoices = Array.from(this.questions).fill(false);
    })

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
