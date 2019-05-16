<template>
  <div class="quiz-container animated flipInX">
    <div class="progress-container">
      <span class="progress">{{progress[0] +1}} of {{progress[1]}}</span>
    </div>
    <div class="question-container">
      <h3 class="question">{{questionData.question}}</h3>
    </div>
    <ul class="answer-container">
      <li
        class="answer-block"
        :class="getRowClass(index)"
        v-for="(choice, index) in questionData.choices"
        @click="answerClicked(index)"
        :key="index"
      >{{choice}}</li>
    </ul>
      <div v-bind:class="{ visible: answer!==null }" class="answer-next-container">
        <div class="answer-explanation">{{questionData.answer.explanation}}</div>
        <div>
          <button class="btn button-advance-question" @click="nextClicked">Next →</button>
        </div>
      </div>
  </div>
</template>

<script>
export default {
  name: "MultipleChoiceShowAnswer",
  data() {
    return {
      answer: null,
      highlight: []
    };
  },
  props: {
    questionData: Object,
    progress: Array
  },
  methods: {
    answerClicked(answerIndex) {
      if (this.answer === null) {
        this.answer = answerIndex;
        let correctAnswer = this.questionData.answer.index;
        this.highlight = this.questionData.choices.map((v, i) => {
          if (i !== correctAnswer && i === answerIndex) {
            return "incorrect";
          } else if (i === correctAnswer) {
            return "correct heartBeat";
          } else {
            return "not-selected";
          }
        });
        this.$emit("answer", { answer: answerIndex });
      }
    },
    nextClicked() {
      this.answer = null;
      this.$emit("nextQuestion");
      this.highlight = this.questionData.choices.map(() => "");
    },
    getRowClass(index) {
      return this.highlight[index];
    }
  }
};
</script>

<style>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}

.answer-block.incorrect {
  background-color: #f44336;
}

.answer-block.correct {
  background-color: #4caf50;
}

.answer-block.not-selected {
  background-color: #9e9e9e;
}

.answer-next-container {
  display: flex;
  margin-top: 30px;
  padding: 0 10px;
  justify-content: space-between;
  border-top: 1px solid #ccc;
  padding-top: 20px;
  visibility:hidden;
}

.answer-next-container.visible{
  visibility:visible;
}

.answer-explanation {
  text-align: left;
  margin-right: 20px;
}

.button-advance-question {
  white-space: nowrap;
}
.animated {
  -webkit-animation-duration: 1s;
  animation-duration: 1s;
  -webkit-animation-fill-mode: both;
  animation-fill-mode: both;
}

.question {
  font-size: 1.5em;
}

@keyframes heartBeat {
  0% {
    -webkit-transform: scale(1);
    transform: scale(1);
  }

  14% {
    -webkit-transform: scale(1.3);
    transform: scale(1.3);
  }

  28% {
    -webkit-transform: scale(1);
    transform: scale(1);
  }

  42% {
    -webkit-transform: scale(1.3);
    transform: scale(1.3);
  }

  70% {
    -webkit-transform: scale(1);
    transform: scale(1);
  }
}

.heartBeat {
  -webkit-animation-name: heartBeat;
  animation-name: heartBeat;
  -webkit-animation-duration: 1.3s;
  animation-duration: 1.3s;
  -webkit-animation-timing-function: ease-in-out;
  animation-timing-function: ease-in-out;
}

@keyframes flipInX {
  from {
    -webkit-transform: perspective(400px) rotate3d(1, 0, 0, 90deg);
    transform: perspective(400px) rotate3d(1, 0, 0, 90deg);
    -webkit-animation-timing-function: ease-in;
    animation-timing-function: ease-in;
    opacity: 0;
  }

  40% {
    -webkit-transform: perspective(400px) rotate3d(1, 0, 0, -20deg);
    transform: perspective(400px) rotate3d(1, 0, 0, -20deg);
    -webkit-animation-timing-function: ease-in;
    animation-timing-function: ease-in;
  }

  60% {
    -webkit-transform: perspective(400px) rotate3d(1, 0, 0, 10deg);
    transform: perspective(400px) rotate3d(1, 0, 0, 10deg);
    opacity: 1;
  }

  80% {
    -webkit-transform: perspective(400px) rotate3d(1, 0, 0, -5deg);
    transform: perspective(400px) rotate3d(1, 0, 0, -5deg);
  }

  to {
    -webkit-transform: perspective(400px);
    transform: perspective(400px);
  }
}

.flipInX {
  -webkit-backface-visibility: visible !important;
  backface-visibility: visible !important;
  -webkit-animation-name: flipInX;
  animation-name: flipInX;
}
</style>

