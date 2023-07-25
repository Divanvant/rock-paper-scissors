<script setup lang="ts">
type TScoreProps = {
  score: number;
};

defineProps<TScoreProps>();
</script>

<template>
  <div class="score-wrapper">
    <div>
      <h1>
        Rock<br />
        Paper<br />
        Scissors
      </h1>
    </div>
    <div class="score">
      <p>Score</p>
      <h2>{{ score }}</h2>
    </div>
  </div>
</template>

<style scoped>
.score-wrapper {
  border: 2px solid var(--headerOutline);
  width: 100%;
  display: flex;
  justify-content: space-between;
  align-items: center;
  border-radius: 0.25rem;
  padding: 0.5rem;
  text-transform: uppercase;
}
h1 {
  font-size: 1.25rem;
  line-height: 0.75;
  text-align: left;
  padding-inline-start: 0.5rem;
  margin: 0;
}
.score {
  padding: 0.5rem 1rem;
  background-color: white;
  line-height: 1;
  border-radius: 0.25rem;
}
.score:not(h2) {
  font-size: 0.75rem;
  font-weight: 700;
  color: var(--scoreText);
}
.score h2 {
  font-size: 2rem;
  color: var(--darkText);
}
</style>
