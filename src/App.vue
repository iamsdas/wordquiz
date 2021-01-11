<template>
  <div>
    <h3>
      high score: {{ highScore }}
      <br />
      score: {{ score }}
    </h3>
  </div>
  <quiz
    :word="word"
    v-on:next-word="getWord()"
    @add-score="increaseScore"
    @reduce-score="decreaseScore"
  />
</template>

<script>
import Quiz from "./components/Quiz.vue";
const randomWords = require("random-words");
export default {
  name: "App",
  components: { Quiz },
  data() {
    return {
      word: "",
      score: 0,
      highScore: 0
    };
  },
  created() {
    if (!localStorage.storedHighScore) {
      localStorage.storedHighScore = this.highScore;
    }
    this.highScore = localStorage.storedHighScore;
    this.getWord();
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
    },
    getWord() {
      this.word = randomWords();
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
