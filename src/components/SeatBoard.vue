<script setup lang="ts">
import DeckSlot from "./DeckSlot.vue";
import { ref, computed } from "vue";
import { StudentCardInfo } from "./DeckPile.vue";
import StudentCard from "./StudentCard.vue";
import SeatSlot from "./SeatSlot.vue";

const props = defineProps<{
  row: number;
  col: number;
  cards: StudentCardInfo[];
}>();

const emits = defineEmits<{
  (e: "confirmSeat", idx: number): void;
}>();

const seatNumber = computed(() => props.row * props.col);
const selectedSeat = ref<number | null>(null);

function selectSeat(idx: number) {
  if (idx === selectedSeat.value) {
    confirmSeat(idx);
    return;
  }
  selectedSeat.value = idx;
}

function confirmSeat(idx: number) {
  emits("confirmSeat", idx);
  selectedSeat.value = null;
}
</script>

<template>
  <div class="seat-board p-4 grid gap-x-1 gap-y-1">
    <seat-slot
      v-for="i in seatNumber"
      @click="selectSeat(i)"
      :selected="selectedSeat === i"
      :student-info="cards[i]?.studentInfo"
    />
  </div>
</template>

<style scoped>
.seat-board {
  grid-template-columns: repeat(v-bind(col), 1fr);
  grid-template-rows: repeat(v-bind(row), 1fr);
}
</style>
