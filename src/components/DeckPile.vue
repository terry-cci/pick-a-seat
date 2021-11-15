<script lang="ts">
import { StudentInfo } from "./StudentCard.vue";

export type StudentCardInfo = {
  studentInfo: StudentInfo;
};
</script>

<script setup lang="ts">
import DeckSlot from "./DeckSlot.vue";

const props = defineProps<{ cards: StudentCardInfo[] }>();
</script>

<template>
  <div>
    <deck-slot class="w-20 h-32" />
  </div>
</template>
