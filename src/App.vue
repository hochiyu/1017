<script setup lang="ts">
import Add from "./components/Add.vue";
import Chemistry from "./components/Chemistry.vue";
import ChemistryRadio from "./components/ChemistryRadio.vue";
import ChemistryCheckbox from "./components/ChemistryCheckbox.vue";
import EnglishCheckbox from "./components/EnglishCheckbox.vue";
import EnglishRadio from "./components/EnglishRadio.vue";
import { ref } from "vue";
let choice = ref("請選擇");
</script>

<template>
  <div>
    <select v-model="choice">
        <option value="Add">加法</option>
      <option value="Chemistry">化學填空</option>
      <option value="ChemistryRadio">化學單選</option>
      <option value="ChemistryCheckbox">化學複選</option>
      <option value="EnglishCheckbox">英文複選</option>
      <option value="EnglishRadio">英文單選</option>
    </select>
    <Add v-if="choice === 'Add'" />
    <Chemistry v-else-if="choice === 'Chemistry'" />
    <ChemistryRadio v-else-if="choice === 'ChemistryRadio'"/>
    <ChemistryCheckbox v-else-if="choice === 'ChemistryCheckbox'" />
    <EnglishCheckbox v-else-if="choice === 'EnglishCheckbox'" />
    <EnglishRadio v-else/>
  </div>
</template>
