<script setup lang="ts">
import { reactive } from "vue";
const state = reactive({ message: "" ,currentQuestion: 0, answer: "" });
let exams = [
  { question: "螞蟻的英文是:", answer: "ant", options: ["ant", "bat", "elephant", "fly"] },
  { question: "蘋果的英文是:", answer: "apple", options: ["apple", "banana", "orange", "grape"] },
  { question: "天空的英文是:", answer: "sky", options: ["sky", "land", "cloud", "sun"] },
  { question: "國文的英文是:", answer: "chinese", options: ["english", "math", "chinese", "chemistry"] },
  { question: "紫色的英文是:", answer: "purple", options: ["purple", "red", "green", "blue"],
  },
];
function generateQuestion() {
    if (exams[state.currentQuestion].answer === state.answer) {
    state.message = "答案正確";
    state.answer = "";
    if (state.currentQuestion + 1 < exams.length) {
      state.currentQuestion++;

    }
  } else {
    state.message = "答案錯誤";
  }

}
</script>
<template>
  {{ exams[state.currentQuestion].question }}
    <span v-for="option in exams[state.currentQuestion].options">
    <input type="radio" v-model="state.answer" :value="option" />
    {{ option }}
  </span>
  {{state.message}}
  <button @click="generateQuestion">下一題
    </button>
</template>