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

<template>
  <div
    class="
      student-card
      bg-blue-50
      rounded
      shadow-sm
      border border-gray-600
      flex flex-col
      justify-center
      items-center
    "
  >
    <h2>{{ studentInfo.name.zh }}</h2>
    <h3 class="text-sm">{{ studentInfo.name.en }} ({{ studentInfo.id }})</h3>
  </div>
</template>
