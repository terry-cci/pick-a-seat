<script setup lang="ts">
import DeckSlot from "./DeckSlot.vue";
import { computed } from "vue";

const props = defineProps<{
  row: number;
  col: number;
}>();

const seatNumber = computed(() => props.row * props.col);
</script>

<template>
  <div class="seat-board p-4 grid gap-x-1 gap-y-1">
    <deck-slot v-for="i in seatNumber" class="border-gray-700" />
  </div>
</template>

<style scoped>
.seat-board {
  grid-template-columns: repeat(v-bind(col), 1fr);
  grid-template-rows: repeat(v-bind(row), 1fr);
}
</style>
