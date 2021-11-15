<script lang="ts">
export type StudentInfo = {
  id: number;
  name: {
    zh: string;
    en: string;
  };
  gender: "M" | "F";
};
</script>

<script setup lang="ts">
const props = defineProps<{
  studentInfo: StudentInfo;
}>();
</script>

<template></template>
