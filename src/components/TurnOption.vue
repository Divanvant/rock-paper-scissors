<script setup lang="ts">
import { Move } from '../App.vue'

export interface TTurnOption {
  loading: boolean
  name: Move
  icon: string
  color: string
}

defineProps<TTurnOption>()
defineEmits(['turnSelected'])
</script>

<template>
  <div class="loading-circle" v-if="loading"></div>
  <button v-else :class="`turn-option ${name}`" @click="$emit('turnSelected')">
    <div class="turn-option-item">
      <img :src="icon" :alt="`Play ${name} this round`" />
    </div>
  </button>
</template>

<style scoped>
.loading-circle,
.turn-option {
  border-radius: 50%;
  background: linear-gradient(hsl(214, 47%, 23%), hsl(237, 49%, 15%));
  width: 8rem;
  aspect-ratio: 1 / 1;
  padding: 1rem;
  overflow: hidden;
}
.turn-option.scissors {
  background: hsl(39, 89%, 49%);
  background: linear-gradient(hsl(40, 84%, 53%), hsl(39, 89%, 49%));
}
.turn-option.paper {
  background: hsl(230, 89%, 62%);
  background: linear-gradient(hsl(230, 89%, 65%), hsl(230, 89%, 62%));
}
.turn-option.rock {
  background: hsl(349, 71%, 52%);
  background: linear-gradient(hsl(349, 70%, 56%), hsl(349, 71%, 52%));
}

.turn-option-item {
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100%;
  height: 100%;
  background-color: white;
}

.loading-circle {
  background: var(--darkText);
  animation: loaderAnimation 0.75s ease-in-out infinite;
}

@keyframes loaderAnimation {
  0%,
  100% {
    opacity: 0;
    transform: scale(0.5);
  }
  50% {
    opacity: 1;
  }
  90% {
    opacity: 1;
  }
  100% {
    opacity: 0;
    transform: scale(1);
  }
}

@media screen and (min-width: 768px) {
  .loading-circle,
  .turn-option {
    width: 12.5rem;
  }
  .turn-option img {
    width: 4.5rem;
  }
}
</style>
