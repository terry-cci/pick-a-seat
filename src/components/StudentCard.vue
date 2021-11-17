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
const props = withDefaults(
  defineProps<{
    studentInfo: StudentInfo;
    shown?: boolean;
  }>(),
  { shown: true }
);
</script>

<template>
  <div
    class="
      bg-blue-50
      rounded
      shadow-sm
      border-2 border-gray-600
      flex flex-col
      justify-center
      items-center
    "
    v-if="shown"
  >
    <h2>{{ studentInfo.name.zh }}</h2>
    <h3 class="text-xs">{{ studentInfo.name.en }} ({{ studentInfo.id }})</h3>
  </div>
  <div
    class="
      rounded
      shadow-sm
      border-2 border-gray-600
      flex flex-col
      justify-center
      items-center
      text-4xl
      font-bold
    "
    :class="[
      studentInfo.gender === 'M'
        ? 'bg-blue-300 text-blue-500'
        : 'bg-pink-300 text-pink-500',
    ]"
    v-else
  >
    ?
  </div>
</template>
