Here is the fully optimized and completely responsive version for your team component (TeamSection.vue).

Key Mobile Enhancements Made:
Layout Scaling (grid-cols-1 md:grid-cols-3): On mobile devices, the columns gracefully stack vertically. Once the screen size hits desktop view (md:), they seamlessly transform into a side-by-side 3-column layout.

Controlled Click Behavior (scale-105 vs scale-110): On phones, using a high scale-110 click zoom can break past the screen boundaries and trigger accidental horizontal site wobbling. The scale has been dynamically tuned (scale-[1.03] md:scale-110) so it scales safely and cleanly on small portrait displays.

Refined Micro-Padding: Reduced the text and box spacing on smaller screens (p-6 sm:p-8 md:p-10) so the card layout looks perfectly centered and doesn't squish elements tightly against the phone's edges.

HTML
<script setup>
import { ref } from 'vue'

const teamMembers = [
  {
    name: 'Khristian Faith A. Tomelden',
    role: 'Creative Director',
    image: 'iyateam.jpg'
  },
  {
    name: 'Reiven R. Balbuena',
    role: 'Back-end Developer',
    image: 'buenateam.jpg'
  },
  {
    name: 'John Andrei P. Manguera',
    role: 'Front-end Developer',
    image: 'dreiteam.jpg'
  }
]

// Track which card is currently active/clicked
const selectedIndex = ref(null)

const selectMember = (index) => {
  // If you click the already active card, it toggles back to normal. Otherwise, it selects the new one.
  selectedIndex.value = selectedIndex.value === index ? null : index
}
</script>

<template>
  <section id="team" class="py-16 sm:py-24 md:py-32 bg-indigo-50/50">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 md:px-12">
      
      <div class="text-center mb-12 sm:mb-16">
        <h2 class="text-3xl sm:text-4xl md:text-5xl font-bold text-slate-900 mb-3 sm:mb-4 tracking-tight">
          Meet the Visionaries
        </h2>
        <p class="text-sm sm:text-base md:text-lg text-slate-500 max-w-2xl mx-auto font-light">
          A specialized trio dedicated to the intersection of art and logic.
        </p>
      </div>

      <div class="grid grid-cols-1 md:grid-cols-3 gap-6 sm:gap-8 lg:gap-10 max-w-sm sm:max-w-xl md:max-w-6xl mx-auto items-center">
        <div 
          v-for="(member, index) in teamMembers" 
          :key="index"
          @click="selectMember(index)"
          :class="[
            'bg-white rounded-2xl p-6 sm:p-8 md:p-10 flex flex-col items-start text-left cursor-pointer select-none transition-all duration-300 ease-out',
            
            // CLICKED STATE: Scales cleanly on mobile without running off-screen, shifts deeper on desktop sizes
            selectedIndex === index 
              ? 'scale-[1.03] md:scale-110 shadow-xl md:shadow-2xl border-2 border-indigo-500 z-10' 
              : 'border border-slate-100 shadow-sm z-0',
            
            // HOVER STATE: Interactive scale lift applied across desktop viewport breakpoints
            selectedIndex !== index 
              ? 'hover:scale-[1.02] md:hover:scale-105 hover:-translate-y-1 hover:shadow-md' 
              : ''
          ]"
        >
          <div 
            :class="[
              'w-20 h-20 sm:w-24 sm:h-24 md:w-28 md:h-28 mb-6 sm:mb-8 rounded-full overflow-hidden shadow-xs border transition-all duration-300',
              selectedIndex === index ? 'border-indigo-200' : 'border-slate-100'
            ]"
          >
            <img 
              :src="member.image" 
              :alt="member.name"
              :class="[
                'w-full h-full object-cover transition-all duration-300',
                selectedIndex === index ? 'grayscale-0' : 'grayscale group-hover:grayscale-0'
              ]"
            />
          </div>
          
          <div class="space-y-3 sm:space-y-4 w-full">
            <h3 class="text-xl sm:text-2xl font-bold text-slate-900 leading-tight tracking-tight">
              {{ member.name }}
            </h3>
            <p 
              :class="[
                'text-[10px] sm:text-xs font-semibold uppercase tracking-widest transition-colors duration-300',
                selectedIndex === index ? 'text-indigo-500' : 'text-slate-400'
              ]"
            >
              {{ member.role }}
            </p>
          </div>
        </div>
      </div>

    </div>
  </section>
</template>