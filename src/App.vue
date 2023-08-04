<script setup lang="ts">
import { ref } from 'vue'
import Score from './components/Score.vue'
import Rules from './components/Rules.vue'
import Button from './components/Button.vue'
import TurnOption, { TTurnOption } from './components/TurnOption.vue'

import paperIcon from './assets/images/icon-paper.svg'
import scissorsIcon from './assets/images/icon-scissors.svg'
import rockIcon from './assets/images/icon-rock.svg'

export type Move = 'rock' | 'paper' | 'scissors'

const score = ref(0)
const userPlayed = ref<Move | null>(null)
const computerPlayed = ref<Move | null>(null)
const result = ref<string>('none')
const loadingResult = ref(false)

const options = [
  { name: 'paper', icon: paperIcon },
  { name: 'scissors', icon: scissorsIcon },
  { name: 'rock', icon: rockIcon },
] as TTurnOption[]

const getOption = (name: string) => {
  const foundItem = options.filter((item) => item.name === name)
  return foundItem[0]
}

const getHouseTurn = () => {
  const houseSelectionIndex = Math.floor(Math.random() * options.length)
  return options[houseSelectionIndex].name
}

const getResult = () => {
  const computerMove = getHouseTurn()
  computerPlayed.value = computerMove

  if (userPlayed.value === computerMove) {
    return 'draw'
  }

  if (
    (userPlayed.value === 'rock' && computerMove === 'scissors') ||
    (userPlayed.value === 'paper' && computerMove === 'rock') ||
    (userPlayed.value === 'scissors' && computerMove === 'paper')
  ) {
    score.value = score.value += 1
    return 'win'
  }

  score.value = score.value -= 1
  return 'lose'
}

const onUsersTurn = (selectedOption: Move) => {
  loadingResult.value = true
  userPlayed.value = selectedOption
  result.value = getResult()
  setTimeout(() => {
    loadingResult.value = false
  }, 1500)
}

const onNewTurn = () => {
  userPlayed.value = null
  computerPlayed.value = null
  result.value = 'none'
}
</script>

<template>
  <Score :loading="loadingResult" :score="score" />

  <div class="page-content">
    <div v-if="userPlayed && computerPlayed" class="turn-details-wrapper">
      <div class="turn-details-item">
        <TurnOption v-bind="getOption(userPlayed)" />
        <h3>You picked</h3>
      </div>
      <div class="turn-details-item">
        <TurnOption
          v-bind="{
            ...getOption(computerPlayed),
            loading: loadingResult,
          }"
        />
        <h3>The house picked</h3>
      </div>

      <transition>
        <div v-if="!loadingResult" class="turn-details-main">
          <h2>You {{ result }}</h2>
          <Button @click="onNewTurn">Play again</Button>
        </div>
      </transition>
    </div>

    <div v-else class="turn-options-wrapper">
      <div
        class="turn-option-wrapper"
        v-for="option in options"
        :key="option.name"
      >
        <TurnOption v-bind="option" @turnSelected="onUsersTurn(option.name)" />
      </div>
    </div>
    <Rules />
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
  background-image: url('./assets/images/bg-triangle.svg');
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
  margin: 0 2rem;
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

.bounce-enter-active {
  animation: bounce-in 0.5s;
}
.bounce-leave-active {
  animation: bounce-in 0.5s reverse;
}
@keyframes bounce-in {
  0% {
    transform: scale(0);
  }
  50% {
    transform: scale(1.25);
  }
  100% {
    transform: scale(1);
  }
}
</style>
