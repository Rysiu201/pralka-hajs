<template>
  <div class="money-loader">
    <label for="amount">Kwota do wyprania:</label>
    <input type="number" v-model="amount" min="100" step="100"/>
    <button @click="emitBills">Generuj banknoty</button>

    <div class="banknotes">
      <img
        v-for="bill in bills"
        :key="bill.id"
        :src="billImage"
        alt="banknot"
        class="banknote"
        draggable="true"
        @dragstart="onDragStart(bill.id, $event)"
      />
    </div>
  </div>
</template>

<script lang="ts" setup>
import { ref } from 'vue'
import billImage from '../assets/black_money.png'

const amount = ref(100)
const bills = ref<{ id: number } []>([])

function removeBill(id: number) {
  bills.value = bills.value.filter(b => b.id !== id)
}

function emitBills() {
  const count = Math.floor(amount.value / 100)
  bills.value = Array.from({ length: count }, (_, i) => ({ id: i }))
}

function onDragStart(id: number, event: DragEvent) {
  event.dataTransfer?.setData('text/plain', id.toString())
}

defineExpose({ removeBill })
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
