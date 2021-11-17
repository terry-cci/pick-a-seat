<script setup lang="ts">
import DeckSlot from "./DeckSlot.vue";
import { ref, computed } from "vue";
import { StudentCardInfo } from "./DeckPile.vue";
import StudentCard from "./StudentCard.vue";

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
  if (props.cards[idx]) return;
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
    <div v-for="i in seatNumber" @click="selectSeat(i)" class="relative">
      <deck-slot
        class="border-gray-700 w-full h-full"
        :class="{
          'border-blue-400 animate-pulse transition-colors': selectedSeat === i,
        }"
      />
      <student-card
        :student-info="cards[i].studentInfo"
        v-if="cards[i]"
        class="absolute inset-0"
      />
    </div>
  </div>
</template>

<style scoped>
.seat-board {
  grid-template-columns: repeat(v-bind(col), 1fr);
  grid-template-rows: repeat(v-bind(row), 1fr);
}
</style>
