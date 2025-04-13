<template>
  <div class="p-2 md:p-4">
    <div class="space-y-3">
      <template v-for="slot in sortedTimeSlots" :key="slot.id">
        <button
          @click="selectTimeSlot(slot)"
          class="group w-full relative"
        >
          <div
            :class="[
              'p-2 md:p-4 rounded-lg border text-left transition-all duration-200',
              'flex items-center justify-between',
              isSelected(slot) 
                ? 'bg-yellow-500 text-white border-yellow-600 transform scale-[1.02]'
                : 'border-gray-200 hover:border-yellow-500 hover:shadow-md',
              getSlotWidthClass(slot)
            ]"
          >
            <div class="flex-1">
              <div class="font-medium flex items-center">
                {{ formatTime(slot.start) }} - {{ formatTime(slot.end) }}
              </div>
              <div 
                class="text-sm mt-1" 
                :class="isSelected(slot) ? 'text-yellow-100' : 'text-gray-500'"
              >
                {{ getDuration(slot) }} hour session
              </div>
            </div>

            
            <!-- Time indicator line
            <div 
              :class="[
                'absolute left-0 top-1/2 -translate-y-1/2 w-1 h-[80%] rounded-full',
                isSelected(slot) ? 'bg-white' : 'bg-yellow-200'
              ]"
            ></div> -->
          </div>
        </button>
      </template>
    </div>
  </div>
</template>

<script setup>
import { computed } from 'vue'

const props = defineProps({
  selectedTime: {
    type: Object,
    default: null
  },
  availableSlots: {
    type: Array,
    required: true
  }
})

const emit = defineEmits(['time-selected'])

const sortedTimeSlots = computed(() => {
  return [...props.availableSlots].sort((a, b) => {
    return new Date(`2000-01-01T${a.start}`) - new Date(`2000-01-01T${b.start}`)
  })
})

const formatTime = (time) => {
  return new Date(`2000-01-01T${time}`).toLocaleTimeString('en-US', {
    hour: 'numeric',
    minute: 'numeric',
    hour12: true
  })
}

const getDuration = (slot) => {
  const start = new Date(`2000-01-01T${slot.start}`)
  const end = new Date(`2000-01-01T${slot.end}`)
  return (end - start) / (1000 * 60 * 60)
}

const getSlotWidthClass = (slot) => {
  const duration = getDuration(slot)
  if (duration >= 2) return 'ml-12'
  if (duration >= 1.5) return 'ml-8'
  return 'ml-4'
}

const showGapIndicator = (slot) => {
  const currentIndex = sortedTimeSlots.value.indexOf(slot)
  if (currentIndex === sortedTimeSlots.value.length - 1) return false
  
  const currentEnd = new Date(`2000-01-01T${slot.end}`)
  const nextStart = new Date(`2000-01-01T${sortedTimeSlots.value[currentIndex + 1].start}`)
  const gapInHours = (nextStart - currentEnd) / (1000 * 60 * 60)
  
  return gapInHours > 0.5
}

const formatGap = (slot) => {
  const currentIndex = sortedTimeSlots.value.indexOf(slot)
  const currentEnd = new Date(`2000-01-01T${slot.end}`)
  const nextStart = new Date(`2000-01-01T${sortedTimeSlots.value[currentIndex + 1].start}`)
  const gapInHours = (nextStart - currentEnd) / (1000 * 60 * 60)
  
  return `${gapInHours} hour gap`
}

const isSelected = (slot) => {
  return props.selectedTime && props.selectedTime.id === slot.id
}

const selectTimeSlot = (slot) => {
  emit('time-selected', slot)
}
</script>

<style scoped>
.dashed-line {
  background-image: linear-gradient(to bottom, #E5E7EB 50%, transparent 50%);
  background-size: 1px 8px;
  background-repeat: repeat-y;
}
</style> 