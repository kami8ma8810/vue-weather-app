<script setup>
import BorderLine from './BorderLine.vue'
defineProps({
  place: Object
})
</script>

<template>
  <div class="text-white p-10 rounded-lg shadow-lg gap-6 mb-6 relative overflow-hidden bg-blue-900">
    <!-- Location & time -->
    <div class="mb-2 flex justify-between items-center">
      <div class="flex items-center justify-center gap-2">
        <i class="fa-solid fa-location-dot"></i>
        <h1 class="text-3xl">{{ place.location.name }}</h1>
      </div>
      <div class="flex items-center justify-center gap-2">
        <i class="fa-solid fa-clock mr-2"></i>
        <h1 class="text-3xl"> {{ new Date(place.location.localtime).getHours().toString().padStart(2, '0') }} : {{ new Date(place.location.localtime).getMinutes().toString().padStart(2, '0') }} </h1>
      </div>
    </div>

    <!-- current weather -->
    <div class="text-center flex-1">
      <img :src="place.current.condition.icon" alt="icon" width="80" class="mx-auto" />
      <h1 class="text-8xl mb-2 relative">{{ Math.round(place.current.temp_c) }}<span class="absolute text-6xl">&deg;</span></h1>
      <p class="text-4xl">{{ place.current.condition.text }}</p>
    </div>

    <BorderLine />

    <!-- forecast -->
    <div>
      <!-- Weather daily forecast component goes here -->
    </div>

    <!-- info -->
    <div>
      <!-- Weather info component goes here -->
    </div>

    <!-- forecast btn -->
    <div class="flex justify-end items-center gap-1 mt-10">
      <button>More <i class="fa-solid fa-arrow-right text-sm -mb-px"></i></button>
    </div>
  </div>
</template>