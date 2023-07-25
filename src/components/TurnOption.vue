<script setup lang="ts">
import { Move } from "../App.vue";

export interface TTurnOption {
  name: Move;
  icon: string;
  color: string;
}

defineProps<TTurnOption>();
defineEmits(["turnSelected"]);
</script>

<template>
  <button :class="`turn-option ${name}`" @click="$emit('turnSelected')">
    <div class="turn-option-item">
      <img :src="icon" :alt="`Play ${name} this round`" />
    </div>
  </button>
</template>

<style scoped>
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

@media screen and (min-width: 768px) {
  .turn-option {
    width: 12.5rem;
  }
  .turn-option img {
    width: 4.5rem;
  }
}
</style>
