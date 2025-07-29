<template>
  <button
    v-if="doorOpen"
    class="red-dot-button door-control"
    @click="emit('toggle')"
  />
</template>

<script lang="ts" setup>
defineProps<{ doorOpen: boolean }>()
const emit = defineEmits<{
  (event: 'toggle'): void
}>()
</script>

<style scoped>
.door-control {
  position: absolute;
  width: 20px;
  height: 20px;
  top: 58%;
  left: 65%;
}
</style>
