<template>
  <header class="bg-gradient-to-r from-blue-600 to-indigo-600 text-white shadow-md sticky top-0 z-50">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="flex justify-between items-center h-16">

        <!-- Logo / Website Name -->
        <div class="flex-shrink-0 flex items-center space-x-2">
          <!-- Optional Logo Icon -->
          <svg class="h-8 w-8 text-orange-400" fill="currentColor" viewBox="0 0 20 20">
            <path d="M11 17a1 1 0 01-1-1v-4H6a1 1 0 010-2h4V6a1 1 0 112 0v4h4a1 1 0 010 2h-4v4a1 1 0 01-1 1z"/>
          </svg>
          <span class="font-bold text-xl sm:text-2xl">TrendCommerce</span>
        </div>

        <!-- Desktop Navigation -->
        <nav class="hidden md:flex space-x-6 font-medium text-white">
          <a href="/" class="hover:text-gray-200 transition-colors">Home</a>
          <a href="/shop" class="hover:text-gray-200 transition-colors">Shop</a>
          <a href="/about" class="hover:text-gray-200 transition-colors">About</a>
          <a href="/contact" class="hover:text-gray-200 transition-colors">Contact</a>
          <a href="/history" class="hover:text-gray-200 transition-colors">History</a>
        </nav>

        <!-- Mobile Hamburger -->
        <div class="md:hidden flex items-center">
          <button @click="isOpen = !isOpen" class="focus:outline-none">
            <svg v-if="!isOpen" class="h-6 w-6" xmlns="http://www.w3.org/2000/svg" fill="none"
              viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
              <path stroke-linecap="round" stroke-linejoin="round" d="M4 6h16M4 12h16M4 18h16"/>
            </svg>
            <svg v-else class="h-6 w-6" xmlns="http://www.w3.org/2000/svg" fill="none"
              viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
              <path stroke-linecap="round" stroke-linejoin="round" d="M6 18L18 6M6 6l12 12"/>
            </svg>
          </button>
        </div>
      </div>
    </div>

    <!-- Mobile Menu -->
    <div v-if="isOpen" class="md:hidden bg-blue-500/90">
      <nav class="px-2 pt-2 pb-4 space-y-1 font-medium text-white">
        <a href="/" class="block px-3 py-2 rounded hover:bg-blue-600 transition-colors">Home</a>
        <a href="/shop" class="block px-3 py-2 rounded hover:bg-blue-600 transition-colors">Shop</a>
        <a href="/about" class="block px-3 py-2 rounded hover:bg-blue-600 transition-colors">About</a>
        <a href="/contact" class="block px-3 py-2 rounded hover:bg-blue-600 transition-colors">Contact</a>
        <a href="/history" class="block px-3 py-2 rounded hover:bg-blue-600 transition-colors">History</a>
      </nav>
    </div>
  </header>
</template>

<script setup>
import { ref } from 'vue'

const isOpen = ref(false)
</script>

<style scoped>
/* Optional: Add smooth transitions for mobile menu */
header nav a {
  transition: color 0.2s ease;
}
</style>
