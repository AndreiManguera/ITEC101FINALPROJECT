<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const isScrolled = ref(false)
const isMobileMenuOpen = ref(false)

const handleScroll = () => {
  isScrolled.value = window.scrollY > 30
}

const toggleMobileMenu = () => {
  isMobileMenuOpen.value = !isMobileMenuOpen.value
  if (isMobileMenuOpen.value) {
    document.body.style.overflow = 'hidden'
  } else {
    document.body.style.overflow = ''
  }
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll)
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
  document.body.style.overflow = ''
})

const scrollToSection = (sectionId) => {
  isMobileMenuOpen.value = false
  document.body.style.overflow = ''
  
  const element = document.getElementById(sectionId)
  if (element) {
    element.scrollIntoView({ behavior: 'smooth' })
  }
}
</script>

<template>
  <nav 
    :class="[
      'fixed top-0 left-0 right-0 z-50 transition-all duration-500 ease-in-out',
      isScrolled || isMobileMenuOpen
        ? 'bg-white/80 backdrop-blur-md shadow-xs border-b border-slate-200/40 py-3' 
        : 'bg-transparent py-5 sm:py-6'
    ]"
  >
    <div class="w-full max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="flex items-center justify-between">
        
        <div 
          @click="scrollToSection('home')"
          class="text-xl font-black text-slate-900 tracking-wider cursor-pointer hover:opacity-80 transition-opacity"
        >
          TRIOTAGAPAYO
        </div>

        <div class="hidden md:flex items-center space-x-8 lg:space-x-12">
          <a @click="scrollToSection('home')" class="text-slate-600 hover:text-indigo-600 font-medium cursor-pointer transition-colors duration-300 relative py-1 group text-sm">
            Home
            <span class="absolute bottom-0 left-0 w-0 h-[2px] bg-indigo-600 transition-all duration-300 group-hover:w-full"></span>
          </a>
          <a @click="scrollToSection('team')" class="text-slate-600 hover:text-indigo-600 font-medium cursor-pointer transition-colors duration-300 relative py-1 group text-sm">
            Team
            <span class="absolute bottom-0 left-0 w-0 h-[2px] bg-indigo-600 transition-all duration-300 group-hover:w-full"></span>
          </a>
          <a @click="scrollToSection('contact')" class="text-slate-600 hover:text-indigo-600 font-medium cursor-pointer transition-colors duration-300 relative py-1 group text-sm">
            Contact
            <span class="absolute bottom-0 left-0 w-0 h-[2px] bg-indigo-600 transition-all duration-300 group-hover:w-full"></span>
          </a>
        </div>

        <div class="flex items-center gap-2 sm:gap-3">
          <button 
            @click="scrollToSection('contact')"
            class="bg-indigo-600 hover:bg-indigo-700 text-white px-4 py-1.5 rounded-lg transition-colors duration-300 font-bold tracking-wider text-[11px] uppercase cursor-pointer"
          >
            Hire Us
          </button>

          <button 
            @click="toggleMobileMenu"
            type="button"
            class="md:hidden w-8 h-8 flex flex-col items-center justify-center text-slate-700 hover:bg-slate-100 rounded-lg transition-colors cursor-pointer relative"
            aria-label="Toggle Navigation Menu"
          >
            <span :class="['w-4 h-0.5 bg-current transition-all duration-300 absolute', isMobileMenuOpen ? 'rotate-45' : '-translate-y-1']"></span>
            <span :class="['w-4 h-0.5 bg-current transition-opacity duration-300', isMobileMenuOpen ? 'opacity-0' : 'opacity-100']"></span>
            <span :class="['w-4 h-0.5 bg-current transition-all duration-300 absolute', isMobileMenuOpen ? '-rotate-45' : 'translate-y-1']"></span>
          </button>
        </div>
        
      </div>
    </div>

    <div 
      :class="[
        'md:hidden fixed inset-x-0 top-[57px] h-[calc(100vh-57px)] bg-white/95 backdrop-blur-lg border-t border-slate-200/50 transition-all duration-300 ease-out z-40 px-6 py-8 flex flex-col justify-start gap-y-6',
        isMobileMenuOpen ? 'opacity-100 translate-y-0' : 'opacity-0 -translate-y-4 pointer-events-none'
      ]"
    >
      <div class="flex flex-col gap-1">
        <span class="text-[10px] font-black tracking-widest text-slate-400 uppercase mb-2">Navigation</span>
        <button @click="scrollToSection('home')" class="w-full text-left text-lg font-bold text-slate-800 hover:text-indigo-600 py-3 border-b border-slate-100 transition-colors">Home</button>
        <button @click="scrollToSection('team')" class="w-full text-left text-lg font-bold text-slate-800 hover:text-indigo-600 py-3 border-b border-slate-100 transition-colors">Team</button>
        <button @click="scrollToSection('contact')" class="w-full text-left text-lg font-bold text-slate-800 hover:text-indigo-600 py-3 border-b border-slate-100 transition-colors">Contact</button>
      </div>

      <div class="mt-auto pb-8 text-left space-y-2">
        <p class="text-xs text-slate-400 font-mono tracking-wider uppercase">© 2026 TRIOTAGAPAYO</p>
        <p class="text-[11px] text-slate-500 font-light leading-relaxed">Student developers from CvSU Naic crafting digital tranquil environments.</p>
      </div>
    </div>
  </nav>
</template>