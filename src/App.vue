<script setup>
import Box from "./components/Box.vue";
import { ref } from "vue";
const character = ref(null);
const count = ref(0);
const history = ref([Array(9).fill(null)]);
const currentSquare = ref(history.value[count.value]);
const nextHistory = ref([...history.value].slice(0, count.value + 1));
const winner = ref(null);
function handlePlay(n) {
  if (currentSquare.value[n - 1] || calculateWinner(currentSquare.value))
    return;
  history.value = nextHistory.value;
  let currentSquareMin = currentSquare.value.slice();
  count.value = history.value.length;
  character.value = count.value % 2 ? "X" : "O";
  currentSquareMin[n - 1] = character.value;
  currentSquare.value = currentSquareMin;
  history.value.push(currentSquare.value);
  if (calculateWinner(currentSquare.value)) {
    winner.value = calculateWinner(currentSquare.value);
  }
}
function undo(n) {
  currentSquare.value = history.value[n];
  nextHistory.value = [...history.value].slice(0, n + 1);
  winner.value = null;
}
function calculateWinner(squares) {
  const lines = [
    [0, 1, 2],
    [3, 4, 5],
    [6, 7, 8],
    [0, 3, 6],
    [1, 4, 7],
    [2, 5, 8],
    [0, 4, 8],
    [2, 4, 6],
  ];
  for (let i = 0; i < lines.length; i++) {
    const [a, b, c] = lines[i];
    if (squares[a] && squares[a] === squares[b] && squares[a] === squares[c]) {
      return squares[a];
    }
  }
  return null;
}
</script>

<template>
  <h1 v-if="winner">Winner is :{{ winner }}</h1>
  <h1 v-else>Next is: {{ count % 2 ? "O" : "X" }}</h1>
  <Box :squares="currentSquare" @onPlay="(n) => handlePlay(n)" />
  <p></p>
  <div>
    <ul v-for="i in count">
      <li>
        <button v-if="i == 1" @click="undo(i - 1)">Go to Start</button>
        <button v-else @click="undo(i - 1)">Go to: {{ i - 1 }}</button>
      </li>
    </ul>
  </div>
</template>

<style scoped>
.status {
  margin-bottom: 10px;
}
.game {
  display: flex;
  flex-direction: row;
}

.game-info {
  margin-left: 20px;
}
</style>
