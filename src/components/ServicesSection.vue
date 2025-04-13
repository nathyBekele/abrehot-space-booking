<template>
  <section class="w-screen bg-white py-10 sm:py-20">
    <div class="mx-4 sm:mx-8 md:mx-16 lg:mx-40">
      <!-- Title and Underline Section -->
      <div class="mb-8 sm:mb-12">
        <h2 class="text-xl sm:text-[26px] font-light mb-2 text-gray-1000">Explore Our Facilities</h2>
        <div class="flex flex-col items-left">
          <div class="h-px bg-gray-200 flex-grow"></div>
          <div class="h-1 bg-yellow-500 w-8"></div>
        </div>
      </div>

      <!-- Facilities Grid -->
      <div class="space-y-8 sm:space-y-16">
        <!-- Facility 1 -->
        <div class="grid grid-cols-1 md:grid-cols-2 bg-[#F2F0EE]">
          <div class="relative h-64 sm:h-96">
            <img 
              src="@/assets/abrehot-2.jpg" 
              alt="Reading Room"
              class="w-full h-full object-cover"
            />
          </div>
          <div class="flex flex-col justify-center p-4 sm:p-10">
            <div class="border-l-4 border-orange-500 pl-4">
              <h2 class="text-base sm:text-lg font-normal text-gray-900">Reference and Leisure Reading Areas</h2>
              <h3 class="text-sm sm:text-base font-bold text-gray-800">Recreational Reading Areas</h3>
            </div>
            
            <p class="pl-5 font-light text-gray-600 text-xs sm:text-sm mt-4">
              Reference and Leisure Reading Areas are designed for light reading in an informal setting.
              Readers select from a wide range of extended texts, including but not exclusive to narrative
              general fiction, nonfiction, picture books, magazines, popular and newly-published items,
              newspapers, comic books, and graphic novels.
            </p>
            
            <!-- Icons -->
            <div class="pl-5 flex space-x-3 mt-4 sm:mt-6">
              <img src="@/assets/no-sound.png" alt="No Sound Icon" class="w-6 h-6 sm:w-8 sm:h-8" />
              <img src="@/assets/no-phone.png" alt="No Sound Icon" class="w-6 h-6 sm:w-8 sm:h-8" />
              <img src="@/assets/no-food.png" alt="No Sound Icon" class="w-6 h-6 sm:w-8 sm:h-8" />
              <img src="@/assets/group.png" alt="No Sound Icon" class="w-6 h-6 sm:w-8 sm:h-8" />
            </div>

            <a href="#" 
              @click.prevent="openReservationModal('Leisure Reading Areas')" 
              class="mt-4 sm:mt-6 pl-5 text-yellow-500 font-semibold hover:text-yellow-600 transition-colors group flex items-center"
            >
              Reserve A Room
              <svg 
                class="w-4 h-4 sm:w-5 sm:h-5 pl-1 transform transition-all duration-200 opacity-0 -translate-x-2 group-hover:opacity-100 group-hover:translate-x-1" 
                fill="none" 
                stroke="currentColor" 
                viewBox="0 0 24 24"
                xmlns="http://www.w3.org/2000/svg"
              >
                <path 
                  stroke-linecap="round" 
                  stroke-linejoin="round" 
                  stroke-width="2" 
                  d="M14 5l7 7m0 0l-7 7m7-7H3"
                />
              </svg>
            </a>
          </div>
        </div>

        <!-- Facility 2 -->
        <div class="grid grid-cols-1 md:grid-cols-2 bg-[#F2F0EE]">
          <div class="flex flex-col justify-center p-4 sm:p-10 order-2 md:order-1">
            <div class="border-l-4 border-orange-500 pl-4">
              <h2 class="text-base sm:text-lg font-normal text-gray-900">Group Study Rooms</h2>
              <h3 class="text-sm sm:text-base font-bold text-gray-800">Collaborative Study Spaces</h3>
            </div>
            
            <p class="ml-5 font-light text-gray-600 text-xs sm:text-sm mt-4">
              Collaborative spaces, designed to facilitate teamwork and collaboration, include group study rooms and designated areas within the Library indicated by signage. Speaking softly is allowed in collaborative areas, but not loud talking. Long cellphone conversations should be done outside of the Library.
            </p>
            
            <!-- Icons -->
            <div class="ml-5 flex space-x-3 mt-4 sm:mt-6">
              <img src="@/assets/no-sound.png" alt="No Sound Icon" class="w-6 h-6 sm:w-8 sm:h-8" />
              <img src="@/assets/no-phone.png" alt="No Sound Icon" class="w-6 h-6 sm:w-8 sm:h-8" />
              <img src="@/assets/no-food.png" alt="No Sound Icon" class="w-6 h-6 sm:w-8 sm:h-8" />
              <img src="@/assets/group.png" alt="No Sound Icon" class="w-6 h-6 sm:w-8 sm:h-8" />
            </div>

            <a href="#" 
              @click.prevent="openReservationModal('Group Study Rooms')" 
              class="mt-4 sm:mt-6 ml-5 text-yellow-500 font-semibold hover:text-yellow-600 transition-colors group flex items-center"
            >
              Reserve A Room
              <svg 
                class="w-4 h-4 sm:w-5 sm:h-5 ml-1 transform transition-all duration-200 opacity-0 -translate-x-2 group-hover:opacity-100 group-hover:translate-x-1" 
                fill="none" 
                stroke="currentColor" 
                viewBox="0 0 24 24"
                xmlns="http://www.w3.org/2000/svg"
              >
                <path 
                  stroke-linecap="round" 
                  stroke-linejoin="round" 
                  stroke-width="2" 
                  d="M14 5l7 7m0 0l-7 7m7-7H3"
                />
              </svg>
            </a>
          </div>
          <div class="relative h-64 sm:h-96 order-1 md:order-2">
            <img 
              src="@/assets/abrehot-4.jpg" 
              alt="Conference Room"
              class="w-full h-full object-cover"
            />
          </div>
        </div>

        <!-- Facility 3 -->
        <div class="grid grid-cols-1 md:grid-cols-2 bg-[#F2F0EE]">
          <div class="relative h-64 sm:h-96">
            <img 
              src="@/assets/abrehot-6.jpg" 
              alt="Study Pods"
              class="w-full h-full object-cover"
            />
          </div>
          <div class="flex flex-col justify-center p-4 sm:p-10">
            <div class="border-l-4 border-orange-500 pl-4">
              <h2 class="text-base sm:text-lg font-normal text-gray-900">Kids & Teens Corner</h2>
              <h3 class="text-sm sm:text-base font-bold text-gray-800">Study & Playgrounds</h3>
            </div>
            
            <p class="ml-5 font-light text-gray-600 text-xs sm:text-sm mt-4">
              The Children's Room contains picture books, board books, beginning readers, early chapter books, fiction books, non-fiction books, and Playaway formats, puzzles, graphic novels, movies and themed literature kits, audio books in CD and DVDs. The collections are designed for age groups ranging from newborns to teens.
            </p>
            
            <!-- Icons -->
            <div class="ml-5 flex space-x-3 mt-4 sm:mt-6">
              <img src="@/assets/no-sound.png" alt="No Sound Icon" class="w-6 h-6 sm:w-8 sm:h-8" />
              <img src="@/assets/no-phone.png" alt="No Sound Icon" class="w-6 h-6 sm:w-8 sm:h-8" />
              <img src="@/assets/no-food.png" alt="No Sound Icon" class="w-6 h-6 sm:w-8 sm:h-8" />
              <img src="@/assets/group.png" alt="No Sound Icon" class="w-6 h-6 sm:w-8 sm:h-8" />
            </div>

            <a href="#" 
              @click.prevent="openReservationModal('Kids & Teens Corner')" 
              class="mt-4 sm:mt-6 ml-5 text-yellow-500 font-semibold hover:text-yellow-600 transition-colors group flex items-center"
            >
              Reserve A Room
              <svg 
                class="w-4 h-4 sm:w-5 sm:h-5 ml-1 transform transition-all duration-200 opacity-0 -translate-x-2 group-hover:opacity-100 group-hover:translate-x-1" 
                fill="none" 
                stroke="currentColor" 
                viewBox="0 0 24 24"
                xmlns="http://www.w3.org/2000/svg"
              >
                <path 
                  stroke-linecap="round" 
                  stroke-linejoin="round" 
                  stroke-width="2" 
                  d="M14 5l7 7m0 0l-7 7m7-7H3"
                />
              </svg>
            </a>
          </div>
        </div>
      </div>
    </div>
  </section>

  <!-- Reservation Modal -->
  <ReservationModal
    :is-open="isModalOpen"
    :facility-type="selectedFacility"
    @close="closeReservationModal"
    @booking-completed="handleBookingCompleted"
  />
</template>

<script setup>
import { ref } from 'vue'
import ReservationModal from './reservation/ReservationModal.vue'

const isModalOpen = ref(false)
const selectedFacility = ref(null)

const openReservationModal = (facilityType) => {
  selectedFacility.value = facilityType
  isModalOpen.value = true
}

const closeReservationModal = () => {
  isModalOpen.value = false
  selectedFacility.value = null
}

const handleBookingCompleted = (bookingDetails) => {
  console.log('Booking completed:', bookingDetails)
  // Remove the alert and let the modal handle the success state
}
</script> 