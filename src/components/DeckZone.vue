<script setup lang="ts">
import DeckPile, { StudentCardInfo } from "./DeckPile.vue";
import { ref } from "vue";
import { StudentInfo } from "./StudentCard.vue";
import S2AStudents from "../data/s2a.json";

const students = S2AStudents as StudentInfo[];

const cards = ref<StudentCardInfo[]>(
  students.map((s) => ({
    studentInfo: s,
  }))
);
</script>

<template>
  <div class="flex flex-col justify-between h-full p-4">
    <deck-pile :cards="[]" />
    <deck-pile :cards="cards" />
  </div>
</template>
