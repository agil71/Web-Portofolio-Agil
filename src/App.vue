<template>
  <div class="app">
    <Navbar @open-contact="openContactModal" />
    <main>
      <HeroSection @open-contact="openContactModal" />
      <WorkGrid />
      <DownloadCVSection />
      <AboutSection />
    </main>
    <FooterSection />
    
    <!-- Contact Modal -->
    <ContactModal :isOpen="isContactModalOpen" @close="closeContactModal" />
  </div>
</template>

<script setup>
import { ref, provide } from 'vue'
import Navbar from './components/Navbar.vue'
import HeroSection from './components/HeroSection.vue'
import WorkGrid from './components/WorkGrid.vue'
import DownloadCVSection from './components/DownloadCVSection.vue'
import AboutSection from './components/AboutSection.vue'
import FooterSection from './components/FooterSection.vue'
import ContactModal from './components/ContactModal.vue'

const isContactModalOpen = ref(false)

// Provide ke semua komponen
provide('openContactModal', () => {
  isContactModalOpen.value = true
})

const openContactModal = () => {
  console.log('Opening modal...') // Untuk debugging
  isContactModalOpen.value = true
}

const closeContactModal = () => {
  console.log('Closing modal...') // Untuk debugging
  isContactModalOpen.value = false
}
</script>

<style>
.app {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  position: relative;
}

main {
  flex: 1;
}
</style>