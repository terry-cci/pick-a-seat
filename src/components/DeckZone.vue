<script setup lang="ts">
import DeckPile, { StudentCardInfo } from "./DeckPile.vue";

const props = withDefaults(
  defineProps<{
    normalCardPile?: StudentCardInfo[];
  }>(),
  { normalCardPile: () => [] }
);
</script>

<template>
  <div class="flex flex-col justify-between h-full p-4">
    <deck-pile />
    <deck-pile :cards="normalCardPile" />
  </div>
</template>
