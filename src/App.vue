<template>
  <div class="app">
    <h1>🧺 Pralnia Pieniędzy 💸</h1>
    <MoneyLoader @bill-thrown="onBillThrown" />
    <WasherDoor :doorOpen="doorOpen" @toggle="doorOpen = !doorOpen" />
    <MoneyStack v-if="doorOpen && !moneyInserted" @insert="moneyInserted = true" />
    <ProgramSelector :selected="program" @select="program = $event" />
    <StartButton
      :canStart="!doorOpen && moneyInserted && program !== null && !washing"
      @start="washing = true"
    />
    <p v-if="washing">Pranie trwa... 🌀</p>
    <Washer :spinning="washing" :doorOpen="doorOpen" />
  </div>
</template>

<script lang="ts" setup>
import { ref } from 'vue'
import WasherDoor from './components/WasherDoor.vue'
import MoneyStack from './components/MoneyStack.vue'
import ProgramSelector from './components/ProgramSelector.vue'
import StartButton from './components/StartButton.vue'
import MoneyLoader from './components/MoneyLoader.vue'
import Washer from './components/Washer.vue'

const doorOpen = ref(true)
const moneyInserted = ref(false)
const program = ref<string | null>(null)
const washing = ref(false)

function onBillThrown(id: number) {
  console.log('wrzuciłeś banknot ${id}')
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