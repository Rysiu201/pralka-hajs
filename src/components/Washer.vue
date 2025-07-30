<template>
  <div class="washer-wrapper">
    <img :src="washerBase" class="washer-base" alt="pralka" />
    <img :src="drumImage" class="washer-drum" :class="{ spinning, visible: spinning }" alt="bęben" />
    <img :src="washerDoor" class="washer-door" :class="{ open: doorOpen }" alt="drzwi" />
    <img v-for="i in billsCount" v-if="spinning" :key="i" src="../assets/black_money.png" class="money-spinning" :style="getMoneyStyle()" alt="pieniądze"/>
    <div v-if="spinning" class="washer-water"></div>
    <div class="washer-dropzone"
        @dragover.prevent
        @drop="onDrop">
    </div>
  </div>
</template>

<script lang="ts" setup>
import washerBase from '../assets/washer_nodoor.png'
import washerDoor from '../assets/washer_door.png'
import drumImage from '../assets/drum.png'

const getMoneyStyle = () => {
  const baseLeft = 33 + Math.random() * 25  // np. 40–60%
  const baseTop = 65 + Math.random() * 13  // np. 45–55%
  const delay = (Math.random() * 0.8).toFixed(2) // 0–0.5s
  const scale = (0.3 + Math.random() * 0.6).toFixed(1)

  return {
    top: `${baseTop}%`,
    left: `${baseLeft}%`,
    transform: `translate(-50%, -50%) scale(${scale})`,
    animationDelay: `${delay}s`,
  }
}

const emit = defineEmits<{
  (e: 'bill-thrown', id: number): void
}>()

function onDrop(event: DragEvent) {
  const id = Number(event.dataTransfer?.getData('text/plain'))
  emit('bill-thrown', id)
}

defineProps<{
  spinning: boolean
  doorOpen: boolean
  billsCount: number
}>()
</script>

<style scoped>
.washer-wrapper {
  position: relative;
  width: 180px;
  height: 180px;
  margin: 0 auto;
  perspective: 600px;
}

.washer-base,
.washer-door,
.washer-drum {
  position: absolute;
  width: 100%;
  top: 0;
  left: 0;
}

.washer-base {
  z-index: 0;
}

.washer-door {
  width: 72%;
  top: 20%;
  left: 15%;
  transform-origin: right center;
  transition: transform 1.5s ease-out;
  transform-style: preserve-3d;
}

.washer-drum {
  position: relative;
  width: 84%;
  top: 28%;
  left: -4%;
  transform-origin: center center;
  z-index: 1;
  will-change: transform;
  opacity: 0;
}

.washer-drum.visible{
  opacity: 1;
}

.washer-door.open {
  transform: rotatey(60deg);
}

.washer-drum.spinning {
  animation: spin 1s linear infinite;
}

.washer-water {
  position: absolute;
  width: 38%;
  height: 28%;
  top: 60%;
  left: 27%;
  background: radial-gradient(circle at 30% 30%, rgba(0, 160, 255, 0.4), rgba(0, 160, 255, 0.2));
  border-radius: 50%;
  z-index: 2;
  pointer-events: none;
  animation: slosh 0.8s ease-in-out infinite;
  filter: blur(1px);
}

.money-spinning{
  position: absolute;
  top: 75%;
  left: 50%;
  width: 25px;
  height: auto;
  z-index: 3;
  transform-origin: center center;
  animation: money-spin 1.6s linear infinite;
  z-index: 2;
}

.washer-dropzone {
  position: absolute;
  width: 100%;
  height: 100%;
  top: 0;
  left: 0;
  z-index: 10;
}
.washer-dropzone.dragover {
  border: 2px dashed #00aaff;
}

@keyframes spin {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(360deg);
  }
}

@keyframes slosh {
  0% {
    transform: rotate(-2deg) skewX(-4deg) scale(1, 1.04) translateY(1px);
  }
  25% {
    transform: rotate(2deg) skewX(3deg) scale(1.02, 1.03) translateY(-2px);
  }
  50% {
    transform: rotate(-1.5deg) skewX(-2deg) scale(1.01, 1.06) translateY(1px);
  }
  75% {
    transform: rotate(1deg) skewX(2deg) scale(1.03, 1.01) translateY(-1px);
  }
  100% {
    transform: rotate(-2deg) skewX(-4deg) scale(1, 1.04) translateY(1px);
  }
}

@keyframes money-spin {
  0% {
    transform: translate(-50%, -50%) rotate(0deg) scale(1);
  }
  50% {
    transform: translate(-50%, -50%) rotate(180deg) scale(1.1);
  }
  100% {
    transform: translate(-50%, -50%) rotate(360deg) scale(1);
  }
}
</style>
