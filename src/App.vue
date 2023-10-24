<script setup lang="ts">
import Add from "./components/Add.vue";
import Chemistry from "./components/Chemistry.vue";
import ChemistryRadio from "./components/ChemistryRadio.vue";
import ChemistryCheckbox from "./components/ChemistryCheckbox.vue";
import EnglishCheckbox from "./components/EnglishCheckbox.vue";
import EnglishRadio from "./components/EnglishRadio.vue";
import English from "./components/EnglishDB.vue";
import { reactive } from "vue";
let choice = reactive({title:'化學', value:"Chemistry"});
let items=[
  {title:'英文', value:"English"},
  {title:'化學', value:"Chemistry"},
  {title:'化學單選', value:"ChemistryRadio"},
  {title:'化學複選', value:"ChemistryCheckbox"},
  {title:'英文單選', value:"EnglishRadio"},
  {title:'英文複選', value:"EnglishCheckbox"}
  ]
</script>

<template>
  <div>
    <v-select label="請選擇" v-model="choice.value" :items="items" item-title="title" item-value="value">
    </v-select>
    <Suspense>
    <Add v-if="choice.value === 'Add'" />
    <Chemistry v-else-if="choice.value === 'Chemistry'" />
    <ChemistryRadio v-else-if="choice.value === 'ChemistryRadio'"/>
    <ChemistryCheckbox v-else-if="choice.value === 'ChemistryCheckbox'" />
    <EnglishCheckbox v-else-if="choice.value === 'EnglishCheckbox'" />
    <EnglishRadio v-else-if="choice.value === 'EnglishRadio'" />
    <English v-else/>
  </Suspense>

  </div>
</template>
