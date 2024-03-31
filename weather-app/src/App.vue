<script setup>
import SearchField from './components/SearchField.vue'
</script>

<template>
  <main>
    <div class="text-center mb-6">
      {{
        new Date()
          .toLocaleDateString('ja-JP', { year: 'numeric', month: '2-digit', day: '2-digit' })
          .replace(/\//g, '/')
      }}
      （{{ ['日', '月', '火', '水', '木', '金', '土'][new Date().getDay()] }}）
    </div>
    <div>
      <SearchField />
    </div>
  </main>
</template>
