<script setup lang="ts">
import { StudentInfo } from "./StudentCard.vue";
import DeckSlot from "./DeckSlot.vue";
import StudentCard from "./StudentCard.vue";

const props = withDefaults(
  defineProps<{
    selected?: boolean;
    studentInfo?: StudentInfo;
  }>(),
  {
    selected: false,
  }
);
</script>

<template>
  <div class="relative">
    <deck-slot
      class="border-gray-700 w-full h-full"
      :class="{
        'border-blue-400 animate-pulse transition-colors':
          selected && !studentInfo,
      }"
    />
    <student-card
      :student-info="studentInfo"
      v-if="studentInfo"
      class="absolute inset-0"
    />
    <span
      class="absolute inset-0 ring ring-transparent rounded transition-colors"
      :class="{ 'ring-red-500 animate-pulse': selected }"
      v-if="studentInfo"
    ></span>
  </div>
</template>
