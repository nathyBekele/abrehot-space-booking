<template>
  <nav class="fixed top-0 left-0 right-0 z-50 bg-white m-0 p-0">
    <div class="container mx-auto px-4 py-4 sm:py-7">
      <div class="flex items-center justify-between">
        <div class="flex flex-col">
          <a href="#" class="text-2xl sm:text-[30px] font-light text-gray-900 leading-none mb-1 hover:text-yellow-500">Abrehot Library</a>
          <div class="text-xs sm:text-[13px] font-light text-gray-500 -mt-1">Ethiopian Public Library</div>
        </div>
        
        <!-- Mobile menu button -->
        <button @click="isMenuOpen = !isMenuOpen" class="md:hidden p-2 rounded-md hover:bg-gray-100">
          <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path v-if="!isMenuOpen" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16"></path>
            <path v-else stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"></path>
          </svg>
        </button>

        <!-- Desktop menu -->
        <div class="hidden md:flex items-center space-x-6">
          <a href="#" class="text-gray-500 hover:text-gray-900 text-[14px] font-normal">Home</a>
          <a href="#" class="text-gray-500 hover:text-gray-900 text-[14px] font-normal">Our Services</a>
          <a href="#" class="text-gray-500 hover:text-gray-900 text-[14px] font-normal">News</a>
          <a href="#" class="text-gray-500 hover:text-gray-900 text-[14px] font-normal">Programs & Events</a>
          <a href="#" class="text-gray-500 hover:text-gray-900 text-[14px] font-normal">Using the Library</a>
          
          <div class="flex space-x-4 ml-4">
            <a href="#" class="p-2 rounded-full bg-gray-100 hover:bg-gray-200 transition-colors duration-300">
              <img src="@/assets/facebook-logo.png" alt="Facebook" class="w-5 h-5" />
            </a>
            <a href="#" class="p-2 rounded-full bg-gray-100 hover:bg-gray-200 transition-colors duration-300">
              <img src="@/assets/twitter-logo.png" alt="Twitter" class="w-5 h-5" />
            </a>
          </div>
        </div>
      </div>

      <!-- Mobile menu -->
      <div v-if="isMenuOpen" class="md:hidden mt-4 pb-4">
        <div class="flex flex-col space-y-4">
          <a href="#" class="text-gray-500 hover:text-gray-900 text-base font-normal">Home</a>
          <a href="#" class="text-gray-500 hover:text-gray-900 text-base font-normal">Our Services</a>
          <a href="#" class="text-gray-500 hover:text-gray-900 text-base font-normal">News</a>
          <a href="#" class="text-gray-500 hover:text-gray-900 text-base font-normal">Programs & Events</a>
          <a href="#" class="text-gray-500 hover:text-gray-900 text-base font-normal">Using the Library</a>
          
          <div class="flex space-x-4 pt-2">
            <a href="#" class="p-2 rounded-full bg-gray-100 hover:bg-gray-200 transition-colors duration-300">
              <img src="@/assets/facebook-logo.png" alt="Facebook" class="w-5 h-5" />
            </a>
            <a href="#" class="p-2 rounded-full bg-gray-100 hover:bg-gray-200 transition-colors duration-300">
              <img src="@/assets/twitter-logo.png" alt="Twitter" class="w-5 h-5" />
            </a>
          </div>
        </div>
      </div>
    </div>
  </nav>
</template>

<script setup>
import { ref } from 'vue'

const isMenuOpen = ref(false)
</script> 