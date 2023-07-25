<script setup lang="ts">
import { ref } from "vue";
import Score from "./components/Score.vue";
import Rules from "./components/Rules.vue";
import Button from "./components/Button.vue";
import TurnOption, { TTurnOption } from "./components/TurnOption.vue";

import paperIcon from "./assets/images/icon-paper.svg";
import scissorsIcon from "./assets/images/icon-scissors.svg";
import rockIcon from "./assets/images/icon-rock.svg";

export type Move = "rock" | "paper" | "scissors";

const score = ref(0);
const userPlayed = ref<Move | null>(null);
const computerPlayed = ref<Move | null>(null);
const result = ref<string>("none");

const options = [
  { name: "paper", color: "hsl(230, 89%, 62%)", icon: paperIcon },
  { name: "scissors", color: "hsl(39, 89%, 49%)", icon: scissorsIcon },
  { name: "rock", color: "hsl(349, 71%, 52%)", icon: rockIcon },
] as TTurnOption[];

const getOption = (name: string) => {
  const foundItem = options.filter((item) => item.name === name);

  return foundItem[0];
};

const getHouseTurn = () => {
  const houseSelectionIndex = Math.floor(Math.random() * options.length);
  return options[houseSelectionIndex].name;
};

const getResult = (userInput: Move) => {
  const computerMove = getHouseTurn();

  userPlayed.value = userInput;
  computerPlayed.value = computerMove;

  if (userInput === computerMove) {
    return "draw";
  }

  if (
    (userInput === "rock" && computerMove === "scissors") ||
    (userInput === "paper" && computerMove === "rock") ||
    (userInput === "scissors" && computerMove === "paper")
  ) {
    score.value = score.value += 1;
    return "win";
  }

  return "lose";
};

const onUsersTurn = (selectedOption: Move) => {
  result.value = getResult(selectedOption);
};

const onNewTurn = () => {
  userPlayed.value = null;
  computerPlayed.value = null;
  result.value = "none";
};
</script>

<template>
  <Score :score="score" />

  <div class="page-content">
    <div v-if="result === 'none'" class="turn-options-wrapper">
      <div
        class="turn-option-wrapper"
        v-for="option in options"
        :key="option.name"
      >
        <TurnOption v-bind="option" @turnSelected="onUsersTurn(option.name)" />
      </div>
    </div>

    <div v-else class="turn-details-wrapper">
      <template v-if="userPlayed && computerPlayed">
        <div class="turn-details-item">
          <TurnOption v-bind="getOption(userPlayed)" />
          <h3>You picked</h3>
        </div>
        <div class="turn-details-item">
          <TurnOption v-bind="getOption(computerPlayed)" />
          <h3>The house picked</h3>
        </div>
      </template>

      <div class="turn-details-main">
        <h2>You {{ result }}</h2>
        <Button @click="onNewTurn">Play again</Button>
      </div>
    </div>

    <div>
      <Rules />
    </div>
  </div>
</template>

<style>
.page-content {
  min-height: calc(100dvh - 80px - 3rem);
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.turn-options-wrapper {
  display: flex;
  flex-flow: row wrap;
  justify-content: center;
  background-image: url("./assets/images/bg-triangle.svg");
  background-repeat: no-repeat;
  background-position: center 75%;
  background-size: 75%;
  padding: 2rem 0;
  margin: 33% auto 0;
  max-width: 480px;
}
.turn-option-wrapper {
  flex: 0 0 50%;
  display: flex;
}
.turn-option-wrapper:nth-of-type(2) {
  justify-content: end;
}
.turn-option-wrapper:nth-of-type(3) {
  margin-block-start: 2rem;
  justify-content: center;
}

.turn-details-wrapper {
  display: flex;
  flex-flow: row wrap;
  justify-content: space-between;
  padding: 2rem 0;
  margin: 33% auto 0;
  max-width: 360px;
}
.turn-details-item {
  text-align: center;
  text-transform: uppercase;
}
.turn-details-item h3 {
  margin-block-start: 1.5rem;
}

.turn-details-main {
  width: 100%;
  text-align: center;
}

.turn-details-main h2 {
  margin-block-start: 1.5rem;
  text-transform: uppercase;
  font-size: 3rem;
  letter-spacing: 1.1px;
}

.turn-details-main button {
  padding-inline: 2.75rem;
  background: white;
  color: var(--darkText);
}

@media screen and (min-width: 768px) {
  .page-content {
    min-height: calc(100dvh - 108px - 3rem);
  }

  .turn-options-wrapper {
    margin: 10% auto 0;
  }
  .turn-details-wrapper {
    margin: 10% auto 0;
    max-width: none;
    align-items: center;
  }
  .turn-details-item {
    display: flex;
    flex-direction: column-reverse;
  }
  .turn-details-item h3 {
    margin-block-end: 2rem;
  }
  .turn-details-main {
    width: max-content;
    order: 2;
    margin-inline: 2rem;
  }
  .turn-details-item:nth-child(1) {
    order: 1;
  }
  .turn-details-item:nth-child(2) {
    order: 3;
  }
}
</style>
