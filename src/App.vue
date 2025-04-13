<script setup>
import Navbar from './components/Navbar.vue'
import HeroSection from './components/HeroSection.vue'
import ServicesSection from './components/ServicesSection.vue'
</script>

<template>
  <div class="w-screen min-h-screen">
    <Navbar />
    <main class="w-screen m-0 p-0">
      <HeroSection/>
      <ServicesSection />
    </main>
  </div>
</template>
