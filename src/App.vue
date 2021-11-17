<script setup lang="ts">
import SeatBoard from "./components/SeatBoard.vue";
import DeckZone from "./components/DeckZone.vue";

import { ref } from "vue";

import { StudentInfo } from "./components/StudentCard.vue";
import S2AStudents from "./data/s2a.json";
import { shuffle } from "./common";
import { StudentCardInfo } from "./components/DeckPile.vue";

const students = S2AStudents as StudentInfo[];

const normalPileCards = ref<StudentCardInfo[]>(
  shuffle(
    students.map((s) => ({
      studentInfo: s,
    }))
  )
);
const boardCards = ref<StudentCardInfo[]>([]);

function confirmSeat(idx: number) {
  if (normalPileCards.value.length > 0 && !boardCards.value[idx]) {
    boardCards.value[idx] = normalPileCards.value.pop() as StudentCardInfo;
  } else if (boardCards.value[idx]) {
    normalPileCards.value.push(boardCards.value[idx]);
    delete boardCards.value[idx];
  }
}
</script>

<template>
  <div class="w-full h-full shadow bg-gray-800 rounded flex">
    <deck-zone :normal-card-pile="normalPileCards" />
    <seat-board
      class="flex-grow"
      :row="5"
      :col="7"
      @confirm-seat="confirmSeat"
      :cards="boardCards"
    />
  </div>
</template>
