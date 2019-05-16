<template>
  <div class="results-container animated slideInUp">
    <h2 class="results-header">{{resultsData.header}}</h2>
    <p class="results-chatter">{{resultsData.chatter}}</p>
    <div class="html-container">
      <div slot="html" v-html="resultsData.html"></div>
    </div>
    <div class="link-container">
      <a class="link" href="https://offers.courier-journal.com/E-F2_D">See more of our Derby drink coverage</a></div>
    <div class="share-container">
      <!--<a href="#">F</a><a href="#">T</a>-->
    </div>
    <div>
      <button class="btn" @click="restartClicked">Try the quiz again!</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "SimpleResults",
  props: {
    quizData: Object,
    quizState: Object
  },
  data() {
    return {
      resultsData: this.quizData.results.answers[this.quizState.resultIndex]
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
.share-container{
  margin:20px;
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