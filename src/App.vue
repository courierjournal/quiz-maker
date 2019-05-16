<template>
  <div id="app">
    <!--Intro Template-->
    <SimpleIntro v-show="quizState.showIntro" v-bind:introData="quizData" v-on:begin="beginQuiz"/>

    <!--Quiz Template-->
    <Jeopardy
      v-if="quizState.showQuiz"
      v-bind:progress="[quizState.currentQuestion, quizState.totalQuestions]"
      v-bind:questionData="quizData.quiz.questions[quizState.currentQuestion]"
      v-on:answer="answerQuestion"
      v-on:nextQuestion="nextQuestion"
    />

    <!--Results Template-->
    <SimpleResultsPercent
      v-if="quizState.showResults"
      v-bind:quizData="quizData"
      v-bind:quizState="quizState"
      v-on:restart="init"
    />
  </div>
</template>

<script>
import data from "./data.json";
import SimpleIntro from "./components/intro/SimpleIntro.vue";
import Jeopardy from "./components/quizzes/Jeopardy.vue";
import SimpleResultsPercent from "./components/results/SimpleResultsPercent.vue";

export default {
  name: "app",
  components: {
    SimpleIntro,
    Jeopardy,
    SimpleResultsPercent
  },
  created() {
    this.init();
  },
  data() {
    return {
      quizData: data,
      quizState: {}
    };
  },
  methods: {
    init() {
      this.quizState = {
        quizType: this.quizData.quiz.template,
        showIntro: true,
        showQuiz: false,
        showResults: false,
        totalQuestions: this.quizData.quiz.questions.length,
        totalCorrect: 0,
        answerHistory: [],
        resultIndex: null,
        currentQuestion: 0
      };
    },
    beginQuiz() {
      //Hide the intro and show the questions
      this.quizState.showIntro = false;
      this.quizState.showQuiz = true;
    },
    answerQuestion(e) {
      //Track the answer
      this.quizState.answerHistory.push(e.answer);
      if (this.quizData.quiz.template === "jeopardy") {
        if (
          e.answer ===
          this.quizData.quiz.questions[this.quizState.currentQuestion].answer
            .index
        ) {
          this.quizState.totalCorrect++;
        }
      } else {
        this.nextQuestion();
      }
    },
    nextQuestion() {
      //Advance to the next question, fire endQuiz() if there are no more
      this.quizState.currentQuestion++;
      if (this.quizState.currentQuestion === this.quizState.totalQuestions) {
        this.endQuiz();
      }
    },
    endQuiz() {
      let answerHistory = this.quizState.answerHistory;
      let highestWeightedIndex = 0;
      if (this.quizState.totalCorrect > 5) {
        highestWeightedIndex = 1;
      }
      if (this.quizState.totalCorrect > 10) {
        highestWeightedIndex = 2;
      }

      this.quizState.resultIndex = highestWeightedIndex;

      //Hide the quiz
      this.quizState.showQuiz = false;
      this.quizState.showResults = true;
    }
  }
};
</script>

<style>
@font-face {
  font-family: "Unify Sans";
  src: url(https://www.gannett-cdn.com/gannett-web/global/fonts/unify/UnifySans_W_Bd.woff2);
  font-weight: 800;
}


:root {
  --gannett-blue: #409bf7;
  --gannett-blue-darker: #1b6cbd;
  --dark-blue: #314fa0;
}

h1,
h2 {
  font-family: "Unify Sans";
}

#app {
  font-family: "Avenir", "Helvetica Neue", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  max-width: 720px;
  margin: 60px auto;
}

.btn {
  font-size: 1.2em;
  font-weight: bold;
  padding: 1em 2em;
  background-color: var(--gannett-blue);
  color: #fff;
  cursor: pointer;
  border: 0;
  transition: 0.3s all;
}

.link,
link:visited,
link:active {
  text-decoration: none;
  border-bottom: 1px dotted;
  color: var(--gannett-blue);
  transition: all 0.3s;
}

.link:hover {
  color: #555;
}

.btn:hover {
  background-color: var(--gannett-blue-darker);
}

.header-description {
  font-size: 1.3em;
}

.answer-container {
  list-style: none;
  padding: 0;
  margin: 0 auto;
}

.answer-block {
  display: block;
  padding: 1em 2em;
  cursor: pointer;
  margin: 10px;
  color: #fff;
  border: 0;
  background-color: var(--dark-blue);
  font-size: 1.1em;
  user-select: none;
  transition: all 0.3s;
}

.answer-block{
  background-color: #ddd;
  color:#333;
  border:1px solid #bbb;
}

.answer-block:hover {
  transform: scale(1.05);
}

.quiz-container {
  max-width: 620px;
  margin: 0 auto;
}

.progress-container {
  text-align: right;
}

.progress {
  background-color: #222;
  color: #fff;
  font-size: 1.2em;
  font-weight: bold;
  border-radius: 20px;
  padding: 4px 10px;
}
</style>
