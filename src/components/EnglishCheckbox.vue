<script setup lang="ts">
import { reactive } from "vue";
const state = reactive({ message: "" ,currentQuestion: 0, answer: [] });
let exams = [
      { question: "哪些字母代表母音?", answer: ["o", "u"], options: ["c", "r", "o", "u"] },
      { question: "哪些字母代表子音?", answer: ["b", "f"], options: ["b", "f", "a", "e"] },
      { question: "那些單詞的中文意思是水果?", answer: ["apple", "banana"], options: ["ant", "apple", "bot", "banana"] },
      { question: "哪些單詞的中文意思是動物?", answer: ["elephant", "rabbit", "penguin"], options: ["bag", "elephant", "rabbit", "penguin"] },
      { question: "哪些單詞的中文意思是顏色?", answer: ["red", "yellow", "purple"], options: ["hello", "purple", "red", "yellow"] }
    ];
    function generateQuestion() {
  if (exams[state.currentQuestion].answer.length === state.answer.length) {
    let correct = 0;
    for (var item of state.answer) {
      if (exams[state.currentQuestion].answer.includes(item)) {
        correct++;
      }
    }
    if (correct == exams[state.currentQuestion].answer.length) {
      state.message = "答案正確";
      if (state.currentQuestion + 1 < exams.length) {
        state.currentQuestion++;
        state.answer = []; //清空上次的答案，否則會讀到上次的值
      }
    } else {
      state.message = "答案錯誤";
    }
  } else {
    state.message = "答案錯誤";
  }
}
</script>
<template>
  {{ exams[state.currentQuestion].question }}
    <span v-for="option in exams[state.currentQuestion].options">
    <input type="checkbox" v-model="state.answer" :value="option" />
    {{ option }}
  </span>
  {{state.message}}
  <button @click="generateQuestion">下一題
    </button>
</template>