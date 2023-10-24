<script setup lang="ts">
import { reactive } from "vue";
import { collection, getDocs, getFirestore } from "firebase/firestore"; 
import app from "@/components/settings/FirebaseConfig.vue"
// Initialize Cloud Firestore and get a reference to the service
const db = getFirestore(app);
const querySnapshot = await getDocs(collection(db, "English"));
// const data = reactive<{question:string, answer:string}[]>([]);
let exams:{question:string, answer:string}[]=[];
querySnapshot.forEach((doc) => {
  exams.push({question:doc.data().question,answer:doc.data().answer});
  console.log(`${doc.id} => ${doc.data()}`);
});
let answer = "";
const state = reactive({ message: "", currentQuestion: 0 });
// let exams = [
//   { question: "氫的化學符號", answer: "H" },
//   { question: "氧的化學符號", answer: "O" },
//   { question: "氦的化學符號", answer: "He" },
// ];
function generateQuestion() {
  if (exams[state.currentQuestion].answer === answer) {
    state.message = "答案正確";
    if (state.currentQuestion + 1 < exams.length) {
      state.currentQuestion++;
    }
  } else {
    state.message = "答案錯誤";
  }

}
generateQuestion();
</script>
<template>
  <div>
    {{ exams[state.currentQuestion].question }}
  
    <input type="text" v-model="answer" />
    {{ state.message }}
    <button @click="generateQuestion">下一題</button>
  </div>
</template>