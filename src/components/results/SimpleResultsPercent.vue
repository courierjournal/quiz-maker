<template>
  <div class="results-container animated slideInUp">
    <h2 class="results-header">You got {{this.percentCorrect}}% correct</h2>
    <p class="results-chatter">{{resultsData.chatter}}</p>
    <div class="html-container">
      <div slot="html" v-html="resultsData.html"></div>
    </div>
    <div class="share-container">
      <FacebookTwitter v-bind:url="quizData.meta.url"/>
    </div>
    <div>
      <button class="btn" @click="restartClicked">Try the quiz again!</button>
    </div>
  </div>
</template>

<script>
import FacebookTwitter from "../share/FacebookTwitter.vue";
export default {
  name: "SimpleResultsPercent",
  components: { FacebookTwitter },
  props: {
    quizData: Object,
    quizState: Object
  },
  data() {
    return {
      resultsData: this.quizData.results.answers[this.quizState.resultIndex],
      percentCorrect: Math.round(
        (this.quizState.totalCorrect / this.quizState.totalQuestions) * 100
      )
    };
  },
  methods: {
    restartClicked() {
      this.$emit("restart");
    }
  }
};
</script>

<style>
.share-container {
  margin: 20px;
}

.results-chatter {
  font-size: 1.4em;
}
.animated {
  -webkit-animation-duration: 1s;
  animation-duration: 1s;
  -webkit-animation-fill-mode: both;
  animation-fill-mode: both;
}

@keyframes slideInUp {
  from {
    -webkit-transform: translate3d(0, 100%, 0);
    transform: translate3d(0, 100%, 0);
    visibility: visible;
  }

  to {
    -webkit-transform: translate3d(0, 0, 0);
    transform: translate3d(0, 0, 0);
  }
}

.slideInUp {
  -webkit-animation-name: slideInUp;
  animation-name: slideInUp;
}
</style>