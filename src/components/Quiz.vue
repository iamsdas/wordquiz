<template>
  <div>
    <h1>{{ word }}</h1>
    <button @click="nextWord()">next</button>
  </div>
  <div>
    <button @click="$emit('add-score')">{{ correctOption }}</button>
    <button @click="$emit('reduce-score')">{{ wrongOption }}</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      correctOption: "",
      wrongOption: ""
    };
  },
  props: {
    word: String
  },
  methods: {
    setOptions() {
      fetch("https://api.datamuse.com/words?rel_ant=" + this.word)
        .then(response => response.json())
        .then(data => {
          if (data.length == 0) this.nextWord();
          else this.correctOption = data[data.length - 1]["word"];
        })
        .catch(err => {
          console.log(err);
        });
      fetch("https://api.datamuse.com/words?rel_syn=" + this.word)
        .then(response => response.json())
        .then(data => {
          if (data.length == 0) this.nextWord();
          else this.wrongOption = data[data.length - 1]["word"];
        })
        .catch(err => {
          console.log(err);
        });
    },
    nextWord() {
      this.$emit("next-word");
    }
  },
  watch: {
    word: {
      handler: "setOptions",
      immediate: true
    }
  }
};
</script>
