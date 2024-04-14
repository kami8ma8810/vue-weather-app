<script setup>
import { ref } from 'vue'
import WeatherForecastDay from './WeatherForecastDay.vue'
import WeatherInfo from './WeatherInfo.vue'
import BorderLine from './BorderLine.vue'

const props = defineProps({
  place: Object
})

const emit = defineEmits(['delete-place'])
const showDetail = ref(false)

const removePlace = (placeName) => {
  emit('delete-place', placeName)
  showDetail.value = !showDetail.value
}
const clickHandler = () => {
  showDetail.value = !showDetail.value
}
</script>

<template>
  <div
    :class="place.current.is_day === 1 ? 'bg-day' : 'bg-night'"
    class="text-white p-4 md:p-8 rounded-lg shadow-lg gap-4 mb-4 relative overflow-hidden"
  >
    <!-- Location & time -->
    <div class="mb-2 flex justify-between items-start gap-2">
      <div class="flex items-center justify-center gap-2">
        <i class="fa-solid fa-location-dot mr-2"></i>
        <h1 class="text-xl md:text-3xl">{{ place.location.name }}</h1>
      </div>
      <div class="flex items-center justify-center gap-2 flex-none">
        <i class="fa-solid fa-clock mr-2"></i>
        <h1 class="text-xl md:text-3xl">
          {{ new Date(place.location.localtime).getHours().toString().padStart(2, '0') }} :
          {{ new Date(place.location.localtime).getMinutes().toString().padStart(2, '0') }}
        </h1>
      </div>
    </div>

    <!-- current weather -->
    <div class="text-center flex-1">
      <img :src="place.current.condition.icon" alt="icon" width="80" class="mx-auto" />
      <h1 class="text-4xl md:text-8xl mb-2 relative">
        {{ Math.round(place.current.temp_c) }}<span class="absolute text-2xl md:text-6xl">&deg;</span>
      </h1>
      <p class="text-xl md:text-4xl">{{ place.current.condition.text }}</p>
    </div>

    <BorderLine />

    <!-- forecast -->
    <div v-for="(day, index) in place.forecast.forecastday" :key="index">
      <WeatherForecastDay :day="day" />
    </div>

    <!-- info -->
    <Transition name="fade">
      <div v-show="showDetail">
        <WeatherInfo
          :place="place"
          @close-info="clickHandler"
          @remove-place="removePlace(place.location.name)"
        />
      </div>
    </Transition>

    <!-- forecast btn -->
    <div class="flex justify-end items-center gap-1 mt-10">
      <button @click="clickHandler">
        More <i class="fa-solid fa-arrow-right text-sm -mb-px"></i>
      </button>
    </div>
  </div>
</template>

<style scoped>
.bg-day {
  background-color: #8ec5fc;
  background-image: linear-gradient(62deg,#d0995a  0%, #3d8ad6 100%);
}
.bg-night {
  background-color: #07223d;
  background-image: linear-gradient(62deg, #16508a 0%, #270845 100%);
}
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.2s ease-out;
}
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
