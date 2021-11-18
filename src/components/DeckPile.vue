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

const CARD_PILING_OFFSET = -1.5;
const cardStyle = (idx: number) => ({
  transform: `translateY(${CARD_PILING_OFFSET * idx}px) rotate(-90deg)`,
});
const indicatorStyle = {
  transform: `translateY(${CARD_PILING_OFFSET * props.cards.length + 30}px)`,
};
</script>

<template>
  <div class="relative flex items-center justify-center">
    <deck-slot class="w-20 h-32" />
    <transition-group
      enter-from-class="bottom-3 opacity-0"
      enter-active-class="transition-all transform duration-300"
      leave-active-class="transition-all transform duration-300"
      leave-to-class="bottom-3 opacity-0"
    >
      <student-card
        v-for="(card, idx) in cards"
        :student-info="card.studentInfo"
        class="absolute w-32 h-20 bottom-0 left-full origin-bottom-left"
        :style="cardStyle(idx)"
        :shown="false"
        :key="card.studentInfo.id"
        :class="{
          'border-gray-700': idx % 2,
        }"
      />
    </transition-group>

    <span
      class="absolute bottom-10 text-gray-50 font-bold"
      :style="indicatorStyle"
      v-if="cards.length"
    >
      {{ cards.length }}
    </span>
  </div>
</template>
