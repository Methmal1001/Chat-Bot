<template>
  <header class="sticky top-0 z-50 bg-white/70 backdrop-blur-md shadow-lg">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="flex justify-between items-center h-16">

        <!-- Logo / Website Name -->
        <div class="flex-shrink-0 flex items-center space-x-2">
          <svg class="h-8 w-8 text-orange-500" fill="currentColor" viewBox="0 0 20 20">
            <path d="M11 17a1 1 0 01-1-1v-4H6a1 1 0 010-2h4V6a1 1 0 112 0v4h4a1 1 0 010 2h-4v4a1 1 0 01-1 1z"/>
          </svg>
          <span class="font-bold text-xl sm:text-2xl text-gray-900">TrendCommerce</span>
        </div>

        <!-- Desktop Navigation -->
        <nav class="hidden md:flex space-x-6 font-medium text-gray-800">
          <a href="/" class="hover:text-blue-600 transition-colors">Home</a>
          <a href="/about" class="hover:text-blue-600 transition-colors">About</a>
          <a href="/contact" class="hover:text-blue-600 transition-colors">Contact</a>
          <a href="/history" class="hover:text-blue-600 transition-colors">History</a>
          
        </nav>

        <!-- Mobile Hamburger -->
        <div class="md:hidden flex items-center">
          <button @click="isOpen = !isOpen" class="focus:outline-none">
            <svg v-if="!isOpen" class="h-6 w-6 text-gray-800" xmlns="http://www.w3.org/2000/svg" fill="none"
              viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
              <path stroke-linecap="round" stroke-linejoin="round" d="M4 6h16M4 12h16M4 18h16"/>
            </svg>
            <svg v-else class="h-6 w-6 text-gray-800" xmlns="http://www.w3.org/2000/svg" fill="none"
              viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
              <path stroke-linecap="round" stroke-linejoin="round" d="M6 18L18 6M6 6l12 12"/>
            </svg>
          </button>
        </div>

      </div>
    </div>

    <!-- Mobile Menu -->
    <transition name="slide-fade">
      <div v-if="isOpen" class="md:hidden bg-white/90 backdrop-blur-sm border-t border-gray-200">
        <nav class="px-4 pt-4 pb-6 space-y-2 font-medium text-gray-800">
          <a href="/" class="block px-3 py-2 rounded hover:bg-blue-50 transition">Home</a>
          <a href="/about" class="block px-3 py-2 rounded hover:bg-blue-50 transition">About</a>
          <a href="/contact" class="block px-3 py-2 rounded hover:bg-blue-50 transition">Contact</a>
          <a href="/history" class="block px-3 py-2 rounded hover:bg-blue-50 transition">History</a>
          
        </nav>
      </div>
    </transition>
  </header>
</template>

<script setup>
import { ref } from 'vue'

const isOpen = ref(false)
</script>

<style scoped>
/* Smooth slide + fade for mobile menu */
.slide-fade-enter-active {
  transition: all 0.3s ease;
}
.slide-fade-leave-active {
  transition: all 0.2s ease;
}
.slide-fade-enter-from {
  opacity: 0;
  transform: translateY(-10px);
}
.slide-fade-enter-to {
  opacity: 1;
  transform: translateY(0);
}
.slide-fade-leave-from {
  opacity: 1;
  transform: translateY(0);
}
.slide-fade-leave-to {
  opacity: 0;
  transform: translateY(-10px);
}
</style>
