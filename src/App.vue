<script setup>
import Navbar from './components/Navbar.vue'
import HeroSection from './components/HeroSection.vue'
import TeamSection from './components/TeamSection.vue'
import KhristianProfile from './components/KhristianProfile.vue'
import ReivenProfile from './components/ReivenProfile.vue'
import AndreiProfile from './components/AndreiProfile.vue'
import ContactSection from './components/ContactSection.vue'
</script>

<template>
  <div>
    <Navbar />
    <HeroSection />
    <TeamSection />
    <hr class="border-gray-200 my-0" />
    <KhristianProfile />
    <hr class="border-gray-200 my-0" />
    <ReivenProfile />
    <hr class="border-gray-200 my-0" />
    <AndreiProfile />
    <hr class="border-gray-200 my-0" />
    <ContactSection />
  </div>
</template>
