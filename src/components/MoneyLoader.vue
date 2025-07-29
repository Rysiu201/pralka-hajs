<template>
  <div class="money-loader">
    <label for="amount">Kwota do wyprania:</label>
    <input type="number" v-model="amount" min="100" step="100"/>
    <button @click="emitBills">Generuj banknoty</button>

    <div class="banknotes">
      <img
        v-for="(bill, index) in bills"
        :key="bill.id"
        :src="billImage"
        alt="banknot"
        class="banknote"
        draggable="true"
        @dragstart="onDragStart(bill.id)"
      />
    </div>
  </div>
</template>

<script lang="ts" setup>
import { ref } from 'vue'
import billImage from '../assets/black_money.png'

const emit = defineEmits<{
  (e: 'bill-thrown', id: number): void
}>()

const amount = ref(100)
const bills = ref<{ id: number } []>([])

function emitBills() {
  const count = Math.floor(amount.value / 100)
  bills.value = Array.from({ length: count }, (_, i) => ({ id: i }))
}

function onDragStart(id: number) {
  event.dataTransfer?.setData('text/plain', id.toString())
}
</script>

<style scoped>
.money-loader {
  margin-bottom: 20px;
}
.banknotes {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
  margin-top: 10px;
}
.banknote {
  width: 50px;
  cursor: pointer;
  transition: transform 0.2s ease;
}
.banknote:hover {
  transform: scale(1.1);
}
</style>
