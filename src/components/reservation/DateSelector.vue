<template>
  <div class="flex flex-col">
    <!-- Calendar section -->
    <div>
      <div class="flex items-center justify-between mb-4 mx-2 md:mx-4">
        <button 
          @click="previousMonth" 
          class="p-2 hover:bg-gray-100 rounded-full transition-colors"
        >
          <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
          </svg>
        </button>
        <h3 class="text-lg font-semibold">{{ currentMonthYear }}</h3>
        <button 
          @click="nextMonth" 
          class="p-2 hover:bg-gray-100 rounded-full transition-colors"
        >
          <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
          </svg>
        </button>
      </div>

      <!-- Days of week -->
      <div class="grid grid-cols-7 md:rounded-lg bg-gray-200 py-2 mb-3">
        <template v-for="day in daysOfWeek" :key="day">
          <div class="text-center text-xs font-medium text-gray-900">
            {{ day }}
          </div>
        </template>
      </div>

      <!-- Calendar grid -->
      <div class="grid grid-cols-7">
        <template v-for="{ date, isCurrentMonth, isAvailable, availableSlots } in calendarDays" :key="date">
          <div class="flex aspect-square w-[60%] h-[60%] md:w-[60%] md:h-[40%] mx-2 md:mx-4 mt-1 items-center justify-center group">
            <button
              @click="selectDate(date)"
              :disabled="!isCurrentMonth || !isAvailable || isPastDate(date)"
              :class="[
                'w-5 h-5 p-4 md:w-8 md:h-8 flex items-center justify-center text-sm transition-all duration-200 rounded-full',
                // Base styles
                isCurrentMonth ? '' : 'opacity-0',
                // Selected state with ring
                isSelected(date) ? 'bg-yellow-600 text-white font-bold ring-2 ring-yellow-600 ring-offset-2' : '',
                // Past dates
                isPastDate(date) && isCurrentMonth ? 'text-gray-300 cursor-not-allowed' : '',
                // Future/present dates with no slots
                !isAvailable && isCurrentMonth && !isPastDate(date) ? 'text-gray-900 cursor-not-allowed' : '',
                // Available dates - same color for all available slots
                isAvailable && isCurrentMonth && !isSelected(date) ? 'bg-yellow-400 font-semibold text-gray-900' : ''
              ]"
            >
              {{ new Date(date).getDate() }}
            </button>

            <!-- Tooltip for available slots -->
            <div
              v-if="isAvailable && isCurrentMonth"
              class="absolute bottom-full left-1/2 transform -translate-x-1/2 px-2 py-1 bg-gray-900 text-white text-xs rounded hidden group-hover:block whitespace-nowrap z-10"
            >
              {{ availableSlots }} slots available
              <div class="absolute bottom-0 left-1/2 transform -translate-x-1/2 translate-y-1/2 rotate-45 w-2 h-2 bg-gray-900"></div>
            </div>
          </div>
        </template>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

const props = defineProps({
  selectedDate: {
    type: String,
    default: null
  },
  availableDates: {
    type: Array,
    required: true
  }
})

const emit = defineEmits(['date-selected'])

const currentDate = ref(new Date())
const daysOfWeek = ['Sun', 'Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat']

const currentMonthYear = computed(() => {
  return currentDate.value.toLocaleDateString('en-US', { month: 'long', year: 'numeric' })
})

const calendarDays = computed(() => {
  const year = currentDate.value.getFullYear()
  const month = currentDate.value.getMonth()
  const firstDay = new Date(year, month, 1)
  const lastDay = new Date(year, month + 1, 0)
  
  // Get days from previous month
  const daysFromPrevMonth = firstDay.getDay()
  const prevMonth = new Date(year, month - 1, 1)
  const daysInPrevMonth = new Date(year, month, 0).getDate()
  
  const days = []
  
  // Add days from previous month
  for (let i = daysInPrevMonth - daysFromPrevMonth + 1; i <= daysInPrevMonth; i++) {
    days.push({
      date: new Date(year, month - 1, i).toISOString().split('T')[0],
      isCurrentMonth: false,
      isAvailable: false,
      availableSlots: 0
    })
  }
  
  // Add days from current month
  for (let i = 1; i <= lastDay.getDate(); i++) {
    const date = new Date(year, month, i).toISOString().split('T')[0]
    const availableDate = props.availableDates.find(d => d.date === date)
    days.push({
      date,
      isCurrentMonth: true,
      isAvailable: availableDate?.hasSlots || false,
      availableSlots: availableDate?.slots || 0
    })
  }
  
  // Add days from next month
  const remainingDays = 42 - days.length // 6 rows * 7 days
  for (let i = 1; i <= remainingDays; i++) {
    days.push({
      date: new Date(year, month + 1, i).toISOString().split('T')[0],
      isCurrentMonth: false,
      isAvailable: false,
      availableSlots: 0
    })
  }
  
  return days
})

const isPastDate = (date) => {
  const today = new Date()
  today.setHours(0, 0, 0, 0)
  return new Date(date) < today
}

const isSelected = (date) => {
  return date === props.selectedDate
}

const selectDate = (date) => {
  emit('date-selected', date)
}

const previousMonth = () => {
  currentDate.value = new Date(
    currentDate.value.getFullYear(),
    currentDate.value.getMonth() - 1,
    1
  )
}

const nextMonth = () => {
  currentDate.value = new Date(
    currentDate.value.getFullYear(),
    currentDate.value.getMonth() + 1,
    1
  )
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600&display=swap');

.aspect-square {
  aspect-ratio: 1 / 1;
}
</style>