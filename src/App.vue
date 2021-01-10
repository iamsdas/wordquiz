<template>
  <div>
    <h3>
      high score: {{ highScore }}
      <br />
      score: {{ score }}
    </h3>
  </div>
  <div>
    <button @click="increaseScore">Add score</button>
    <button @click="decreaseScore">Decrease score</button>
  </div>
</template>

<script>
export default {
  name: "App",
  components: {},
  data() {
    return {
      score: 0,
      highScore: 0
    };
  },
  created() {
    if (!localStorage.storedHighScore) {
      localStorage.storedHighScore = this.highScore;
    }
    this.highScore = localStorage.storedHighScore;
  },
  watch: {
    highScore(newHighScore) {
      localStorage.storedHighScore = newHighScore;
    },
    score(newScore) {
      if (newScore > this.highScore) this.highScore = newScore;
    }
  },
  methods: {
    increaseScore() {
      this.score += 100;
    },
    decreaseScore() {
      this.score -= 150;
    }
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
