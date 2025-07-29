<template>
  <div>
    <button :disabled="!canStart" @click="emit('start')">
      ▶️ Start prania
    </button>
  </div>
</template>

<script lang="ts" setup>
defineProps<{ canStart: boolean }>()
const emit = defineEmits<{
  (event: 'start'): void
}>()
</script>
