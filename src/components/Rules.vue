<script setup lang="ts">
import { ref } from "vue";

import Button from "../components/Button.vue";

import closeIcon from "../assets/images/icon-close.svg";
import rules from "../assets/images/image-rules.svg";

const showRulesModal = ref<boolean>(false);

const toggleRulesModal = () => {
  showRulesModal.value = !showRulesModal.value;
};
</script>

<template>
  <div class="rules-section">
    <Button @click="toggleRulesModal" class="btn-white-outlined">Rules</Button>

    <div v-show="showRulesModal" class="rules-modal">
      <h2>Rules</h2>

      <img :src="rules" alt="Rules of the game" />

      <Button @click="toggleRulesModal">
        <img :src="closeIcon" alt="Close Icon" />
      </Button>
    </div>
  </div>
</template>

<style scoped>
.rules-section {
  display: flex;
  align-items: center;
  justify-content: center;
}

.rules-modal {
  position: fixed;
  inset: 0;
  background: white;
  color: var(--darkText);
  display: flex;
  text-align: center;
  flex-direction: column;
  justify-content: space-between;
  align-items: center;
  padding-block: 2rem;
}
.rules-modal h2 {
  text-transform: uppercase;
}
.rules-modal button {
  background: transparent;
}
</style>
