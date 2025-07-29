<template>
  <div class="app">
    <h1>🧺 Pralnia Pieniędzy 💸</h1>
    <MoneyLoader ref="loader" />
    <Washer
      :spinning="washing"
      :doorOpen="doorOpen"
      @bill-thrown="onBillThrown"
    />
    <WasherDoor
      v-if="moneyInserted"
      :doorOpen="doorOpen"
      @toggle="doorOpen = !doorOpen"
    />
    <ProgramSelector
      v-if="moneyInserted && !doorOpen"
      :selected="program"
      @select="program = $event"
    />
    <StartButton
      v-if="!doorOpen && moneyInserted && program !== null"
      :canStart="!washing"
      @start="startWashing"
    />
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

function onBillThrown(id: number) {
  moneyInserted.value = true
  loader.value?.removeBill(id)
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
</style>