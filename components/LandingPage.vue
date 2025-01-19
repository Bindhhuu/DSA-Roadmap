<template>
  <div
    class="landing-container"
    :style="{ backgroundImage: `url(${require('@/assets/frontp.jpg')})` }"
  >
    <h1 class="animated-text">
      <span v-for="(word, index) in words" :key="index" :class="{ blink: word === 'CodeCrafters' && blinking }">
        {{ word }}
      </span>
    </h1>
    <button
      v-if="showStartButton"
      class="start-button"
      @click="navigateToFrontPage"
    >
      Start
    </button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      words: ['Hi', 'CodeCrafters!', "Let's", 'get', 'Started'],
      currentWordIndex: 0,
      blinking: false,
      showStartButton: false,
    };
  },
  mounted() {
    this.animateText();
  },
  methods: {
    animateText() {
      const interval = setInterval(() => {
        if (this.currentWordIndex < this.words.length) {
          this.currentWordIndex++;
          if (this.words[this.currentWordIndex - 1] === 'CodeCrafters!') {
            this.blinking = true;
            setTimeout(() => {
              this.blinking = false;
            }, 1000);
          }
        } else {
          clearInterval(interval);
          this.showStartButton = true;
        }
      }, 100); // 1-second delay between words
    },
    navigateToFrontPage() {
      this.$router.push('/frontpage');
    },
  },
};
</script>

<style scoped>
.landing-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  background-size: cover;
  background-position: center;
  color: black;
  text-align: center;
  display: flex;
  flex-direction: column;
  min-height: 100vh;
  
  display: flex;
  flex-direction: column;
  background-size: cover; /* Ensures the image covers the container */
}

.animated-text {
  font-size: 2rem;
  font-weight: bold;
  animation: fadeIn 1s ease-in-out;
}

.animated-text span {
  opacity: 0;
  animation: appear 1s forwards;
  display: inline-block;
  margin: 0 5px;
}

.blink {
  animation: blink 1s step-end infinite;
}

@keyframes appear {
  from {
    opacity: 0;
    transform: translateY(10px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@keyframes blink {
  50% {
    opacity: 0;
  }
}

.start-button {
  margin-top: 20px;
  padding: 10px 20px;
  font-size: 1.2rem;
  background-color: lavender;
  color: black;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.start-button:hover {
  background-color: darkorchid;
  color: white;
}
</style>
