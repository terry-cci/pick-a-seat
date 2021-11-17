<script lang="ts">
import { StudentInfo } from "./StudentCard.vue";

export type StudentCardInfo = {
  studentInfo: StudentInfo;
};
</script>

<script setup lang="ts">
import DeckSlot from "./DeckSlot.vue";
import StudentCard from "./StudentCard.vue";

const props = withDefaults(defineProps<{ cards?: StudentCardInfo[] }>(), {
  cards: () => [],
});

const CARD_PILING_OFFSET = -0.5;
const cardStyle = (idx: number) => ({
  transform: `translateY(${CARD_PILING_OFFSET * idx}px) rotate(-90deg)`,
});
</script>

<template>
  <div class="relative">
    <deck-slot class="w-20 h-32" />
    <student-card
      v-for="(card, idx) in cards"
      :student-info="card.studentInfo"
      class="absolute w-32 h-20 origin-top-left"
      :style="cardStyle(idx)"
    />
  </div>
</template>
