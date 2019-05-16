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
        v-for="(choice, index) in questionData.choices"
        @click="answerClicked(index)"
        :key="index"
      >{{choice}}</li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "MultipleChoiceWeighted",
  data() {
    return {
      answer: null
    };
  },
  props: {
    questionData: Object,
    progress: Array
  },
  methods: {
    answerClicked(answerIndex) {
      this.$emit("answer", { answer: answerIndex });
      this.answer = null;
    }
  }
};
</script>

<style>
.animated {
  -webkit-animation-duration: 1s;
  animation-duration: 1s;
  -webkit-animation-fill-mode: both;
  animation-fill-mode: both;
}

.question {
  font-size: 1.5em;
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

