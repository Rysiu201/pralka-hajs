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
  width: 6%;
  height: 6%;
  top: 25.5%;
  right: 68.5%;
  border-style: solid;
  border-radius: 3vh;
  border-color: forestgreen;
  border-width: 1px;
}
</style>
