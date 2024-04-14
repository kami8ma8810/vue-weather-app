<script setup>
import {ref } from 'vue'
import SearchField from './components/SearchField.vue'
import WeatherCard from './components/WeatherCard.vue'

const places = ref([])

const addPlace = (data) => {
  places.value.push(data)
}

const deletePlace = (name) =>{
  places.value = places.value.filter(place => place.location.name !== name)
}
</script>

<template>
  <main>
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
      <SearchField @place-data="addPlace"/>
    </div>
    <!-- Weather Cards -->
    <div class="grid grid-cols-2 gap-4 mt-8">
      <div v-for="(place,index) in places" :key="index">
        <WeatherCard :place="place" @delete-place="deletePlace"/>
      </div>
    </div>
  </main>
</template>
