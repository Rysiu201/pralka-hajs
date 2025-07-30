<template>
  <div class="app">
    <h1>🧺 Pralnia Pieniędzy 💸</h1>
    <MoneyLoader ref="loader" />
    <div class="washer-container">
      <Washer
        :spinning="washing"
        :doorOpen="doorOpen"
        @bill-thrown="onBillThrown"
      />
      <WasherDoor
        v-if="moneyInserted && doorOpen"
        :doorOpen="doorOpen"
        @toggle="doorOpen = false"
      />
      <button
        v-if="moneyInserted && !doorOpen && !showProgramMenu"
        class="red-dot-button program-toggle"
        @click="showProgramMenu = true"
      />
      <ProgramSelector
        v-if="showProgramMenu"
        :selected="program"
        @select="selectProgram"
      />
      <StartButton
        v-if="program !== null && !doorOpen && !washing"
        :canStart="true"
        @start="startWashing"
      />
      <div class="counter" v-if="insertedCount > 0">{{ insertedCount }}</div>
    </div>
    <p v-if="washing">Pranie trwa... 🌀</p>
  </div>
</template>

<script lang="ts" setup>
import { ref } from 'vue'
import WasherDoor from './components/WasherDoor.vue'
import ProgramSelector from './components/ProgramSelector.vue'
import StartButton from './components/StartButton.vue'
import MoneyLoader from './components/MoneyLoader.vue'
import Washer from './components/Washer.vue'

const doorOpen = ref(true)
const moneyInserted = ref(false)
const program = ref<string | null>(null)
const washing = ref(false)
const loader = ref<InstanceType<typeof MoneyLoader> | null>(null)
const insertedCount = ref(0)
const showProgramMenu = ref(false)

function onBillThrown(id: number) {
  moneyInserted.value = true
  insertedCount.value += 1
  loader.value?.removeBill(id)
}

function selectProgram(p: string) {
  program.value = p
  showProgramMenu.value = false
}

function startWashing(){
  washing.value = true
  setTimeout(() => {
    washing.value =false
  }, 5000)
}
</script>

<style scoped>
.app {
  text-align: center;
  padding: 2rem;
  font-family: sans-serif;
}

.washer-container {
  position: relative;
  width: fit-content;
  margin: 0 auto;
}

.program-toggle {
  font-size: 10px;
  text-align: center;
  position: absolute;
  top: 26.9%;
  left: 40%;
  width: 4.1%;
  height: 1.9%;
  border-radius: 10px; /* brak zaokrągleń = kwadrat */
  transform: translateX(-50%);
  box-shadow: 0 0 2px rgba(0, 0, 0, 0.5);
}

.counter {
  position: absolute;
  font-size: 5px;
  color: aquamarine;
  top: 28.7%;
  right: 31%;
  padding: 0.2rem 0.4rem;
  border-radius: 4px;
}
</style>