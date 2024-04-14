<script setup>
import { ref } from 'vue'
import SearchField from './components/SearchField.vue'
import WeatherCard from './components/WeatherCard.vue'

const places = ref([])

const addPlace = (data) => {
  places.value.push(data)
}

const deletePlace = (name) => {
  if (confirm('Are you sure you want to delete this location?')) {
    places.value = places.value.filter((place) => place.location.name !== name)
  }
}
</script>

<template>
  <main>
    <div class="flex items-baseline justify-center gap-4 mb-8">
      <i class="fa-solid fa-dog text-2xl"></i>
      <h1 class="text-center text-2xl md:text-4xl">ワンニャン Weather</h1>
      <i class="fa-solid fa-cat text-2xl icon-cat"></i>
    </div>
    <!-- Date -->
    <div class="text-center mb-6">
      {{
        new Date()
          .toLocaleDateString('ja-JP', { year: 'numeric', month: '2-digit', day: '2-digit' })
          .replace(/\//g, '/')
      }}
      （{{ ['日', '月', '火', '水', '木', '金', '土'][new Date().getDay()] }}）
    </div>
    <!-- Search -->
    <div>
      <SearchField @place-data="addPlace" />
    </div>
    <!-- Weather Cards -->
    <div class="grid md:grid-cols-2 gap-4 mt-8">
      <div v-for="(place, index) in places" :key="index">
        <WeatherCard :place="place" @delete-place="deletePlace" />
      </div>
    </div>
  </main>
</template>

<style scoled>
.icon-cat{
  transform: rotateY(180deg);
}
</style>
