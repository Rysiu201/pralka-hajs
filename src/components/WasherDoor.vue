<template>
  <div>
    <p>Drzwi pralki są: <strong>{{ doorOpen ? 'Otwarte' : 'Zamknięte' }}</strong></p>
    <button @click="emit('toggle')">
      {{ doorOpen ? 'Zamknij drzwi' : 'Otwórz drzwi' }}
    </button>
  </div>
</template>

<script lang="ts" setup>
const props = defineProps<{ doorOpen: boolean }>()
const emit = defineEmits<{
  (event: 'toggle'): void
}>()
</script>
