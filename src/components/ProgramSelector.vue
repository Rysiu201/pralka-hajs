<template>
  <div class="program-menu">
    <p>🧼 Wybierz program:</p>
    <button
      v-for="p in programs"
      :key="p"
      :style="{ fontWeight: selected === p ? 'bold' : 'normal' }"
      @click="$emit('select', p)"
    >
      {{ p }}
    </button>
  </div>
</template>

<script lang="ts" setup>
defineProps<{ selected: string | null }>()
defineEmits<{
  (e: 'select', program: string): void
}>()

const programs = ['Kryptowaluty', 'Fundacja', 'Sztuka', 'Zagraniczny przelew']
</script>

<style scoped>
.program-menu {
  position: absolute;
  top: -60px;
  left: 50%;
  transform: translateX(-50%);
  background: white;
  padding: 0.5rem 1rem;
  border-radius: 4px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
}
</style>
