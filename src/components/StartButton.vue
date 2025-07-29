<template>
  <button
    class="red-dot-button start-control"
    :disabled="!canStart"
    @click="emit('start')"
  />
</template>

<script lang="ts" setup>
defineProps<{ canStart: boolean }>()
const emit = defineEmits<{
  (event: 'start'): void
}>()
</script>

<style scoped>
.start-control {
  position: absolute;
  top: -10px;
  right: -10px;
}
</style>
