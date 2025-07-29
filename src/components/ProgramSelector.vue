<template>
  <div>
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
const props = defineProps<{ selected: string | null }>()
defineEmits<{
  (e: 'select', program: string): void
}>()

const programs = ['Kryptowaluty', 'Fundacja', 'Sztuka', 'Zagraniczny przelew']
</script>
