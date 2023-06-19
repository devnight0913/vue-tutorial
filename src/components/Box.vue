<script setup>
const props = defineProps({
  squares: Array,
});
const emit = defineEmits(['onPlay']);
import Square from "./square.vue";
</script>

<template>
  <div class="board-row">
    <Square :sing="props.squares[0]" @click="emit('onPlay',1)" />
    <Square :sing="props.squares[1]" @click="emit('onPlay',2)" />
    <Square :sing="props.squares[2]" @click="emit('onPlay',3)" />
  </div>
  <div class="board-row">
    <Square :sing="props.squares[3]" @click="emit('onPlay',4)" />
    <Square :sing="props.squares[4]" @click="emit('onPlay',5)" />
    <Square :sing="props.squares[5]" @click="emit('onPlay',6)" />
  </div>
  <div class="board-row">
    <Square :sing="props.squares[6]" @click="emit('onPlay',7)" />
    <Square :sing="props.squares[7]" @click="emit('onPlay',8)" />
    <Square :sing="props.squares[8]" @click="emit('onPlay',9)" />
  </div>
</template>

<style scoped>
.board-row:after {
  clear: both;
  content: "";
  display: table;
}
</style>
