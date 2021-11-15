<script setup lang="ts">
import SeatBoard from "./components/SeatBoard.vue";
import DeckZone from "./components/DeckZone.vue";
</script>

<template>
  <div class="w-full h-full shadow bg-gray-800 rounded flex">
    <deck-zone />
    <seat-board class="flex-grow" :row="5" :col="7" />
  </div>
</template>
