<template>
  <div>
    <div class="share-text">Share this quiz:</div>
    <div>
      <a class="share-icon-link" v-bind:href="getFacebookUrl()" target="_blank">
        <svg height="67" width="67" xmlns="http://www.w3.org/2000/svg">
          <path
            d="M29.765 50.32h6.744V33.998h4.499l.596-5.624h-5.095l.007-2.816c0-1.466.14-2.253 2.244-2.253h2.812V17.68h-4.5c-5.405 0-7.307 2.729-7.307 7.317v3.377h-3.369v5.625h3.369V50.32zM34 64C17.432 64 4 50.568 4 34 4 17.431 17.432 4 34 4s30 13.431 30 30c0 16.568-13.432 30-30 30z"
            fill-rule="evenodd"
            clip-rule="evenodd"
            fill="#3a589b"
          ></path>
        </svg>
      </a>
      <a class="share-icon-link" v-bind:href="getTwitterUrl()" target="_blank">
        <svg height="67" width="67" xmlns="http://www.w3.org/2000/svg">
          <path
            d="M38.167 22.283c-2.619.953-4.274 3.411-4.086 6.101l.063 1.038-1.048-.127c-3.813-.487-7.145-2.139-9.974-4.915l-1.383-1.377-.356 1.017c-.754 2.267-.272 4.661 1.299 6.271.838.89.649 1.017-.796.487-.503-.169-.943-.296-.985-.233-.146.149.356 2.076.754 2.839.545 1.06 1.655 2.097 2.871 2.712l1.027.487-1.215.021c-1.173 0-1.215.021-1.089.467.419 1.377 2.074 2.839 3.918 3.475l1.299.444-1.131.678a11.751 11.751 0 0 1-5.616 1.567c-.944.021-1.719.106-1.719.17 0 .211 2.557 1.397 4.044 1.864 4.463 1.377 9.765.783 13.746-1.568 2.829-1.674 5.657-5 6.978-8.221.713-1.715 1.425-4.851 1.425-6.354 0-.975.063-1.102 1.236-2.267.692-.678 1.341-1.419 1.467-1.631.21-.403.188-.403-.88-.043-1.781.636-2.033.551-1.152-.402.649-.678 1.425-1.907 1.425-2.267 0-.063-.314.042-.671.233-.377.212-1.215.53-1.844.72l-1.131.361-1.027-.7c-.566-.381-1.361-.805-1.781-.932-1.069-.296-2.704-.254-3.668.085zM34 64C17.432 64 4 50.568 4 34 4 17.431 17.432 4 34 4s30 13.431 30 30c0 16.568-13.432 30-30 30z"
            fill-rule="evenodd"
            clip-rule="evenodd"
            fill="#598dca"
          ></path>
        </svg>
      </a>
    </div>
  </div>
</template>

<script>
export default {
  name: "SimpleResultsPercent",
  props: {
    url: String
  },
  methods: {
    getFacebookUrl() {
      return (
        "https://www.facebook.com/sharer/sharer.php?u=" +
        encodeURIComponent(this.url)
      );
    },
    getTwitterUrl() {
      return "https://twitter.com/home?status=" + encodeURIComponent(this.url);
    }
  }
};
</script>

<style scoped>
.share-text {
  font-weight: bold;
}

.share-icon-link {
  display: inline-block;
  margin: 0 10px;
}
svg {
  transform:scale(1);
  transition: transform 0.3s;
}

.share-icon-link:hover > svg {
  transform: scale(1.1);
}
</style>