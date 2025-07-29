<template>
  <div class="money-stack">
    <img
      src="../assets/money.png"
      class="money"
      :class="{ inserted: inserted }"
      @click="handleInsert"
      alt="banknot"
    />
    <p>Kliknij, aby wrzucić pieniądze</p>
  </div>
</template>

<script lang="ts" setup>
import { ref } from 'vue'

const emit = defineEmits<{
  (event: 'insert'): void
}>()

const inserted = ref(false)

function handleInsert() {
  inserted.value = true
  setTimeout(() => {
    emit('insert')
  }, 700)
}
</script>

<style scoped>
.money-stack {
  margin: 1rem;
}
.money {
  width: 100px;
  cursor: pointer;
  transition: transform 0.7s ease-in;
}
.money.inserted {
  transform: translateY(150px) rotate(720deg);
  opacity: 0;
}
</style>
