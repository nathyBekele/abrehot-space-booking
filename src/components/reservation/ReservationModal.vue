<template>
  <div v-if="isOpen" class="fixed inset-0 z-50">
    <!-- Fixed overlay -->
    <div class="fixed inset-0">
      <div 
        class="absolute inset-0 bg-gray-500 bg-opacity-75 transition-opacity" 
        @click="closeModal"
      ></div>
    </div>

    <!-- Fixed size modal container -->
    <div class="fixed inset-0 flex items-center justify-center p-4">
      <div 
        class="bg-white rounded-lg shadow-xl w-full max-w-lg flex flex-col relative h-[60vh] md:h-[90vh] max-h-[700px]"
      >
        <!-- Fixed header -->
        <div class="flex-shrink-0 px-6 py-4">
          <div class="flex justify-between items-center">
            <h3 v-if="!showSuccess" class="text-lg font-medium text-gray-900">
              {{ modalTitle }}
            </h3>
            <button @click="closeModal" class="text-gray-600 hover:text-gray-500 ml-auto">
              <span class="sr-only">Close</span>
              <svg class="h-5 w-5" fill="none" viewBox="0 0 25 25" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="3" d="M6 18L18 6M6 6l12 12" />
              </svg>
            </button>
          </div>
          
          <div v-if="!showSuccess" class="h-px bg-gray-100 mt-2"></div>

          <!-- Step navigation -->
          <div v-if="!showSuccess" class="flex justify-between mt-2 md:mt-5 mx-auto md:mx-2 md:space-x-4">
            <div 
              v-for="(step, index) in steps" 
              :key="index"
              class="flex-1 relative"
            >
              <div 
                :class="[
                  'text-center text-sm rounded-lg',
                  currentStep > index ? 'text-yellow-500 font-semibold' : 'text-gray-400'
                ]"
              >
                {{ step }}
              </div>
              <div 
                :class="[
                  'h-1 mt-2 transition-all duration-200 rounded-lg',
                  currentStep >= index ? 'bg-yellow-500' : 'bg-gray-200'
                ]"
              ></div>
            </div>
          </div>
        </div>

        <!-- Content area -->
        <div v-if="!showSuccess" class="flex-1">
          <div class="mx-auto mt-2">
            <!-- Calendar Step -->
            <DateSelector
              v-if="currentStep === 0"
              :selected-date="selectedDate"
              :available-dates="availableDates"
              @date-selected="handleDateSelected"
              class="md:mx-8 md:mt-5"
            />

            <!-- Time Slots Step -->
            <div v-if="currentStep === 1" class="overflow-y-auto h-[calc(50vh-120px)] md:h-[calc(90vh-200px)]">
              <TimeSlotSelector
                :selected-time="selectedTime"
                :available-slots="availableTimeSlots"
                @time-selected="handleTimeSelected"
                class="mx-2 md:mx-4 mb-2"
              />
            </div>

            <!-- User Details Step -->
            <UserDetailsForm
              v-if="currentStep === 2"
              ref="userDetailsFormRef"
              :selected-date="selectedDate"
              :selected-time="selectedTime"
              :facility-type="facilityType"
              @booking-completed="handleBooking"
            />
          </div>
        </div>

        <!-- Success Message -->
        <!-- <div v-else class="flex-1 flex items-center justify-center">
          <div class="flex flex-col items-center justify-center">
            <div class="w-20 h-20 bg-green-100 rounded-full flex items-center justify-center mb-6 shadow-lg shadow-green-100/50">
              <svg class="w-10 h-10 text-green-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2.5" d="M5 13l4 4L19 7" />
              </svg>
            </div>
            <h3 class="text-2xl font-bold text-gray-900 mb-4">Booking Successful!</h3>
            <div class="text-gray-500 text-center space-y-2">
              Your space has been successfully booked. We'll send you a confirmation email shortly.
            </div>
            <div class="mt-8 flex items-center gap-2 text-green-600">
              <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z" />
              </svg>
              <span class="text-sm">You'll receive the email shortly</span>
            </div>
          </div>
        </div> -->

        <div v-else class="flex flex-col items-center justify-center py-16 px-8 rounded-2xl">
          <div class="w-20 h-20 bg-green-100 rounded-full flex items-center justify-center mb-6 shadow-lg shadow-green-100/50">
            <svg class="w-10 h-10 text-green-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2.5" d="M5 13l4 4L19 7" />
            </svg>
          </div>
          <h3 class="text-2xl font-bold text-gray-900 mb-4">Booking Successful!</h3>
          <div class="text-gray-500 text-center space-y-2">
            Your space has been successfully booked. We'll send you a confirmation email shortly.
          </div>
          <div class="mt-8 flex items-center gap-2 text-green-600">
            <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z" />
            </svg>
            <span class="text-sm">You'll receive the email shortly</span>
          </div>
        </div>

        <!-- Fixed footer -->
        <div v-if="!showSuccess" class="absolute bottom-0 left-0 right-0 px-6 py-4 bg-[#F2F0EE] rounded-b-lg">
          <div class="flex flex-row-reverse gap-3">
            <button
              v-if="currentStep < 2"
              @click="nextStep"
              :disabled="!canProceed"
              class="inline-flex justify-center rounded-md border border-transparent px-4 py-2 bg-yellow-500 text-base font-medium text-white hover:bg-yellow-600 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-yellow-500 sm:text-sm disabled:opacity-50 disabled:cursor-not-allowed"
            >
              Next
            </button>
            <button
              v-if="currentStep === 2"
              @click="handleBooking"
              :disabled="!canProceed"
              class="inline-flex justify-center rounded-md border border-transparent px-4 py-2 bg-yellow-500 text-base font-medium text-white hover:bg-yellow-600 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-yellow-500 sm:text-sm disabled:opacity-50 disabled:cursor-not-allowed"
            >
              Book Space
            </button>
            <button
              v-if="currentStep > 0"
              @click="previousStep"
              class="inline-flex justify-center rounded-md border border-gray-300 px-4 py-2 bg-white text-base font-medium text-gray-700 hover:bg-gray-50 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-yellow-500 sm:text-sm"
            >
              Back
            </button>
            <button
              @click="closeModal"
              class="inline-flex justify-center rounded-md border border-gray-300 px-4 py-2 bg-white text-base font-medium text-gray-700 hover:bg-gray-50 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-yellow-500 sm:text-sm"
            >
              Cancel
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, watch, onBeforeUnmount } from 'vue'
import DateSelector from './DateSelector.vue'
import TimeSlotSelector from './TimeSlotSelector.vue'
import UserDetailsForm from './UserDetailsForm.vue'

// Props
const props = defineProps({
  isOpen: {
    type: Boolean,
    required: true
  },
  facilityType: {
    type: String,
    required: true
  }
})

// Emits
const emit = defineEmits(['close', 'booking-completed'])

// State
const currentStep = ref(0)
const selectedDate = ref(null)
const selectedTime = ref(null)

// Mock data - replace with API calls later
const availableDates = ref([
  { date: '2025-04-24', hasSlots: true, slots: 6 },
  { date: '2025-04-28', hasSlots: true, slots: 8 },
  { date: '2025-04-29', hasSlots: true, slots: 3 },
  { date: '2025-04-30', hasSlots: true, slots: 4 }
])

const availableTimeSlots = ref([
  { id: 1, start: '09:00', end: '10:00' },
  { id: 2, start: '10:00', end: '11:00' },
  { id: 3, start: '11:30', end: '12:30' },
  { id: 4, start: '14:00', end: '15:00' },
  { id: 5, start: '15:00', end: '16:00' },
  { id: 6, start: '16:30', end: '17:30' }
])

// Computed
const steps = ['Select Date', 'Choose Time', 'Your Details']

const modalTitle = computed(() => {
  switch (currentStep.value) {
    case 0:
      return 'Select Available Date'
    case 1:
      return 'Choose Time Slot'
    case 2:
      return 'Enter Your Details'
    default:
      return 'Reserve a Room'
  }
})

const canProceed = computed(() => {
  switch (currentStep.value) {
    case 0:
      return selectedDate.value !== null
    case 1:
      return selectedTime.value !== null
    case 2:
      return true // Always true for the summary step
    default:
      return false
  }
})

// Watch for modal open/close to handle body scroll
watch(() => props.isOpen, (isOpen) => {
  if (isOpen) {
    document.body.style.overflow = 'hidden'
    document.body.style.paddingRight = `${window.innerWidth - document.documentElement.clientWidth}px` // Prevent layout shift
  } else {
    document.body.style.overflow = ''
    document.body.style.paddingRight = ''
  }
})

// Cleanup on component unmount
onBeforeUnmount(() => {
  document.body.style.overflow = ''
  document.body.style.paddingRight = ''
})

// Methods
const showSuccess = ref(false)

const closeModal = () => {
  emit('close')
  resetForm()
  showSuccess.value = false
}

const nextStep = () => {
  if (currentStep.value < steps.length - 1) {
    currentStep.value++
  }
}

const previousStep = () => {
  if (currentStep.value > 0) {
    currentStep.value--
  }
}

const resetForm = () => {
  currentStep.value = 0
  selectedDate.value = null
  selectedTime.value = null
  showSuccess.value = false
}

const handleDateSelected = (date) => {
  selectedDate.value = date
}

const handleTimeSelected = (time) => {
  selectedTime.value = time
}

const userDetailsFormRef = ref(null)

const handleBooking = async () => {
  try {
    // Emit the booking event to the parent
    emit('booking-completed', {
      date: selectedDate.value,
      time: selectedTime.value,
      facilityType: props.facilityType
    })
    
    // Show success message
    showSuccess.value = true
  } catch (error) {
    console.error('Booking failed:', error)
  }
}
</script>

<style>
.modal-open {
  overflow: hidden !important;
}
</style> 