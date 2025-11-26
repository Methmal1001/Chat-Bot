<template>
  <div class="max-w-4xl mx-auto mt-10 p-6">
    <h1 class="text-3xl font-bold text-gray-800 mb-6 text-center">
      Chat History
    </h1>

    <!-- Loading Skeleton -->
    <div v-if="loading" class="space-y-4">
      <div class="h-24 bg-gray-200 animate-pulse rounded-xl"></div>
      <div class="h-24 bg-gray-200 animate-pulse rounded-xl"></div>
      <div class="h-24 bg-gray-200 animate-pulse rounded-xl"></div>
    </div>

    <!-- No Data -->
    <div v-else-if="history.length === 0" class="text-center text-gray-500">
      No chat history found.
    </div>

    <!-- Chat History List -->
    <div v-else class="space-y-6">
      <div
        v-for="item in history"
        :key="item.id"
        class="bg-white shadow-md rounded-xl p-5 border border-gray-100 hover:shadow-lg transition"
      >
        <!-- Top row -->
        <div class="flex items-center justify-between mb-3">
          <h2 class="font-semibold text-gray-700 text-lg">
            Conversation #{{ item.id }}
          </h2>
          <span class="text-sm text-gray-500">{{ formatDate(item.createdAt) }}</span>
        </div>

        <!-- User Message -->
        <div class="mb-3">
          <div class="flex items-center gap-2 text-blue-600 font-semibold">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none"
              viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
              <path stroke-linecap="round" stroke-linejoin="round"
                d="M12 11c0-.552-.448-1-1-1H5c-.552 0-1 .448-1 1v6c0 .552.448 1 1 1h6c.552 0 1-.448 1-1v-6zm8-8h-6c-.552 0-1 .448-1 1v6c0 .552.448 1 1 1h6c.552 0 1-.448 1-1V4c0-.552-.448-1-1-1z" />
            </svg>
            User
          </div>
          <p class="ml-7 text-gray-800">{{ item.userMessage }}</p>
        </div>

        <!-- Bot Message -->
        <div>
          <div class="flex items-center gap-2 text-green-600 font-semibold">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none"
              viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
              <path stroke-linecap="round" stroke-linejoin="round"
                d="M19 11H5m14 0c.552 0 1 .448 1 1v6c0 .552-.448 1-1 1H5c-.552 0-1-.448-1-1v-6c0-.552.448-1 1-1m14 0V7a2 2 0 00-2-2h-3" />
            </svg>
            Bot
          </div>
          <p class="ml-7 text-gray-800">{{ item.botMessage }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
definePageMeta({
  ssr: false   // ⬅ prevents Nuxt SSR memory crash
})

import { ref, onMounted } from 'vue'

const history = ref([])
const loading = ref(true)

onMounted(async () => {
  try {
    const res = await fetch('https://localhost:7155/history') // your .NET API
    history.value = await res.json()
  } catch (e) {
    console.error("Failed to load history", e)
  } finally {
    loading.value = false
  }
})

function formatDate(dt) {
  return new Date(dt).toLocaleString()
}
</script>

<style scoped>
div {
  animation: fade 0.2s ease-in;
}

@keyframes fade {
  from { opacity: 0; }
  to { opacity: 1; }
}
</style>
