<script setup>
import { ref, computed } from 'vue'

const teamA = ref("Falcons")
const teamB = ref("Tigers")
const scoreA = ref(0)
const scoreB = ref(0)
const step = ref(1) // points added per click
const maxScore = ref(10)

// true once either team has reached the winning score
const gameOver = computed(() => scoreA.value >= maxScore.value || scoreB.value >= maxScore.value)

function addA() {
  if (gameOver.value) return // stop scoring once someone has already won
  scoreA.value = Math.min(maxScore.value, scoreA.value + step.value)
}

function addB() {
  if (gameOver.value) return
  scoreB.value = Math.min(maxScore.value, scoreB.value + step.value)
}

function reset() {
  scoreA.value = 0
  scoreB.value = 0
}
</script>

<template>
  <div style="font-family: Arial; max-width: 520px; margin: 24px auto;">
    <h2>Mini Scoreboard</h2>

    <p><strong>{{ teamA }}</strong> vs <strong>{{ teamB }}</strong></p>

    <p>Current: {{ scoreA }} - {{ scoreB }}</p>

    <p>Total points: {{ scoreA + scoreB }}</p>
    <p>Points left to win: {{ maxScore - Math.max(scoreA, scoreB) }}</p>

    <div style="display: flex; gap: 12px; margin: 12px 0;">
      <button @click="addA">+ Team A</button>
      <button @click="addB">+ Team B</button>
      <button @click="reset">Reset</button>
    </div>

    <div style="margin-top: 14px;">
      <p v-if="gameOver">Winner: {{ scoreA > scoreB ? teamA : teamB }}</p>
    </div>
  </div>
</template>

<style scoped>
p,
input {
  font-family: monospace;
}

p {
  white-space: pre;
}
</style>