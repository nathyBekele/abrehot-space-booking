<template>
  <form @submit.prevent="handleSubmit" class="max-w-lg bg-white px-8 user-details-form">
    <!-- <h2 class="mb-2 font-semibold">Memebership Details</h2> -->
    <div v-if="!showSuccess">
      <!-- <div class="bg-blue-50 border-l-4 py-4 px-2 border-blue-600 flex items-center justify-left mb-4">
        <svg class="w-5 h-5 text-blue-600 mx-auto" fill="none" stroke="currentColor" viewBox="0 0 24 24">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 16h-1v-4h-1m1-4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
        </svg>
        <div>
          <p class="text-blue-700 text-sm">
            Please review your booking details
          </p>
        </div>
      </div> -->
      
      <div class="space-y-6">
        <!-- Date Summary -->
        <div class="form-group">
          <label class="block text-sm font-medium text-gray-700 mb-1">
            Selected Date
          </label>
          <div class="relative">
            <div class="absolute inset-y-0 left-0 pl-3 flex items-center pointer-events-none">
              <svg class="h-5 w-5 text-gray-400" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 7V3m8 4V3m-9 8h10M5 21h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v12a2 2 0 002 2z" />
              </svg>
            </div>
            <div class="block w-full pl-10 pr-4 py-3 border border-gray-300 rounded-lg sm:text-sm">
              {{ formatDate(selectedDate) }}
            </div>
          </div>
        </div>

        <!-- Time Summary -->
        <div class="form-group">
          <label class="block text-sm font-medium text-gray-700 mb-1">
            Selected Time
          </label>
          <div class="relative">
            <div class="absolute inset-y-0 left-0 pl-3 flex items-center pointer-events-none">
              <svg class="h-5 w-5 text-gray-400" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z" />
              </svg>
            </div>
            <div class="block w-full pl-10 pr-4 py-3 border border-gray-300 rounded-lg sm:text-sm">
              {{ formatTime(selectedTime) }}
            </div>
          </div>
        </div>

        <!-- Facility Summary -->
        <div class="form-group">
          <label class="block text-sm font-medium text-gray-700 mb-1">
            Facility Type
          </label>
          <div class="relative">
            <div class="absolute inset-y-0 left-0 pl-3 flex items-center pointer-events-none">
              <svg class="h-5 w-5 text-gray-400" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 21V5a2 2 0 00-2-2H7a2 2 0 00-2 2v16m14 0h2m-2 0h-5m-9 0H3m2 0h5M9 7h1m-1 4h1m4-4h1m-1 4h1m-5 10v-5a1 1 0 011-1h2a1 1 0 011 1v5m-4 0h4" />
              </svg>
            </div>
            <div class="block w-full pl-10 pr-4 py-3 border border-gray-300 rounded-lg sm:text-sm">
              {{ facilityType }}
            </div>
          </div>
        </div>
      </div>
    </div>

  </form>
</template>

<script setup>
import { ref } from 'vue'

const props = defineProps({
  selectedDate: {
    type: String,
    required: true
  },
  selectedTime: {
    type: Object,
    required: true
  },
  facilityType: {
    type: String,
    required: true
  }
})

const emit = defineEmits(['booking-completed'])

const showSuccess = ref(false)

// Expose the showSuccess ref to parent components
defineExpose({
  showSuccess
})

const formatDate = (dateString) => {
  const date = new Date(dateString)
  return date.toLocaleDateString('en-US', { 
    weekday: 'long',
    year: 'numeric',
    month: 'long',
    day: 'numeric'
  })
}

const formatTime = (timeSlot) => {
  if (!timeSlot) return ''
  return `${timeSlot.start} - ${timeSlot.end}`
}

// Remove the handleSubmit function since we're handling the booking in the parent
</script>

<style scoped>
input:-webkit-autofill,
input:-webkit-autofill:hover,
input:-webkit-autofill:focus {
  -webkit-box-shadow: 0 0 0px 1000px white inset;
  transition: background-color 5000s ease-in-out 0s;
}
</style>