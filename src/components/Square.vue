<script setup>
const props = defineProps({
  sing: String,
});
</script>

<template>
  <button class="square">{{ props.sing }}</button>
</template>

<style scoped>
.square {
  background: #fff;
  border: 1px solid #999;
  float: left;
  font-size: 3vw;
  font-weight: bold;
  line-height: 34px;
  margin-right: -1px;
  margin-top: -1px;
  padding: 0;
  text-align: center;
  height: 5vw;
  width: 5vw;
}
</style>
