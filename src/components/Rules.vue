<script setup lang="ts">
import { ref } from "vue";
import closeIcon from "../assets/images/icon-close.svg";
import rules from "../assets/images/image-rules.svg";

const showRulesModal = ref<boolean>(false);

const toggleRulesModal = () => {
  showRulesModal.value = !showRulesModal.value;
};
</script>

<template>
  <button @click="toggleRulesModal">Rules</button>

  <div v-show="showRulesModal" class="rules-modal">
    <h2>Rules</h2>

    <img :src="rules" alt="Rules of the game" />

    <button @click="toggleRulesModal">
      <img :src="closeIcon" alt="Close Icon" />
    </button>
  </div>
</template>

<style scoped>
.rules-modal {
  position: fixed;
  inset: 0;
  background: white;
  color: var(--darkText);
  display: flex;
  text-align: center;
  flex-direction: column;
  justify-content: space-around;
  align-items: center;
}
.rules-modal h2 {
  text-transform: uppercase;
}
.rules-modal button {
  background: transparent;
}
</style>
