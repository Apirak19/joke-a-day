<script setup lang="ts">
import TheJoke from "../components/TheJoke.vue";
import TodayComponent from "@/components/TodayComponent.vue";
</script>

<template>
  <main class="w-full flex flex-col items-center gap-8 text-3xl">
    <h1 class="text-5xl font-bold text-wrap ">JokeADayMakePainGoesAway</h1>
    <TodayComponent />
    <TheJoke />
  </main>
</template>

