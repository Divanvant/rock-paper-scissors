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

    <div v-show="showRulesModal" class="rules-modal-wrapper">
      <div class="rules-modal">
        <div>
          <h2>Rules</h2>
        </div>

        <img :src="rules" alt="Rules of the game" />

        <Button class="close-button" @click="toggleRulesModal">
          <img :src="closeIcon" alt="Close Icon" />
        </Button>
      </div>
    </div>
  </div>
</template>

<style scoped>
.rules-section {
  display: flex;
  align-items: center;
  justify-content: center;
}

.rules-modal-wrapper {
  z-index: 9;
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
  line-height: 1;
  text-transform: uppercase;
}
.rules-modal button {
  background: transparent;
}

@media screen and (min-width: 768px) {
  .rules-section {
    justify-content: flex-end;
  }
  .rules-modal {
    width: 400px;
    height: 400px;
    inset: 50% auto auto 50%;
    transform: translate(-50%, -50%);
    padding: 2rem;
    text-align: left;
    align-items: flex-start;
    border-radius: 0.25rem;
  }
  .rules-modal-wrapper {
    position: fixed;
    inset: 0;
    background-color: hsla(0, 0%, 0%, 0.4);
  }

  .rules-modal img {
    margin: 0 auto;
  }

  .close-button {
    position: absolute;
    inset: 2rem 2rem auto auto;
    padding: 0;
  }
}
</style>
