<script setup>
import { ref } from 'vue'

const scrollToTeam = () => {
  const element = document.getElementById('team')
  if (element) {
    element.scrollIntoView({ behavior: 'smooth' })
  }
}

// 3D Hover Effect for Image
const imageWrapperRef = ref(null)
const imageTransform = ref('rotateX(0deg) rotateY(0deg)')

const handleImageMouseMove = (e) => {
  // Prevent calculations on touch devices to ensure stable layout performance
  if (window.matchMedia('(pointer: coarse)').matches) return

  const card = imageWrapperRef.value
  if (!card) return

  const rect = card.getBoundingClientRect()
  const x = e.clientX - rect.left 
  const y = e.clientY - rect.top 
  
  const centerX = rect.width / 2
  const centerY = rect.height / 2
  
  const rotateY = ((x - centerX) / centerX) * 6 
  const rotateX = ((centerY - y) / centerY) * 6 

  imageTransform.value = `rotateX(${rotateX}deg) rotateY(${rotateY}deg)`
}

const handleImageMouseLeave = () => {
  imageTransform.value = 'rotateX(0deg) rotateY(0deg)'
}
</script>

<template>
  <section id="home" class="min-h-[100dvh] flex items-center bg-white pt-20 pb-12 sm:pt-28 sm:pb-20 relative overflow-hidden">
    
    <div class="absolute inset-0 z-0 overflow-hidden pointer-events-none opacity-60 sm:opacity-85 mix-blend-multiply">
      <div class="absolute top-[-5%] left-[-15%] sm:left-[-5%] w-[280px] h-[280px] sm:w-[550px] sm:h-[550px] rounded-full bg-indigo-200/40 blur-[40px] sm:blur-[80px] animate-blob"></div>
      <div class="absolute bottom-[5%] right-[-10%] sm:right-[-5%] w-[320px] h-[320px] sm:w-[650px] sm:h-[650px] rounded-full bg-sky-200/40 blur-[50px] sm:blur-[90px] animate-blob animation-delay-2000"></div>
      <div class="absolute top-[40%] left-[15%] sm:left-[30%] w-[250px] h-[250px] sm:w-[500px] sm:h-[500px] rounded-full bg-violet-100/30 blur-[40px] sm:blur-[70px] animate-blob animation-delay-4000"></div>
    </div>

    <div class="w-full max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-4 sm:py-12 relative z-10">
      <div class="grid grid-cols-1 lg:grid-cols-12 gap-10 lg:gap-12 xl:gap-20 items-center">
        
        <div class="space-y-6 sm:space-y-8 lg:col-span-7 order-2 lg:order-1 text-left">
          <div class="space-y-3 sm:space-y-5">
            
            <div class="inline-flex items-center gap-2 bg-indigo-50 px-3 py-1 rounded-full border border-indigo-100/80 mb-1 mx-auto lg:mx-0">
              <span class="w-1.5 h-1.5 rounded-full bg-indigo-600"></span>
              <p class="text-indigo-600 font-black text-[10px] uppercase tracking-widest">We code. We design. We ship.</p>
            </div>
            
            <h1 class="text-3xl sm:text-4xl md:text-5xl xl:text-6xl font-black text-slate-900 leading-[1.15] sm:leading-[1.1] tracking-tight">
              Crafting digital experiences with serenity and precision.
            </h1>
          </div>
          
          <p class="text-sm sm:text-base md:text-lg text-slate-600 max-w-2xl font-light leading-relaxed">
            We blend minimalist aesthetics with high-performance web engineering to build digital tools that feel as fluid as they look.
          </p>
          
          <div class="pt-2 sm:pt-4">
            <button 
              @click="scrollToTeam"
              class="w-full sm:w-auto relative overflow-hidden group/btn bg-indigo-600 text-white px-6 py-3.5 sm:px-8 sm:py-4 rounded-xl transition-all duration-300 font-bold text-xs sm:text-sm tracking-wider cursor-pointer shadow-md shadow-indigo-600/10 hover:shadow-lg hover:shadow-indigo-600/20 hover:-translate-y-0.5"
            >
              <span class="absolute inset-0 w-full h-full bg-gradient-to-r from-indigo-700 to-violet-700 opacity-0 group-hover/btn:opacity-100 transition-opacity duration-300"></span>
              <span class="relative flex items-center justify-center gap-2">
                EXPLORE PORTFOLIO 
                <svg class="w-4 h-4 group-hover/btn:translate-x-1 transition-transform duration-300" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M14 5l7 7m0 0l7-7m-7 7H3"></path>
                </svg>
              </span>
            </button>
          </div>
        </div>

        <div 
          ref="imageWrapperRef"
          class="w-full lg:col-span-5 order-1 lg:order-2 overflow-visible max-w-sm sm:max-w-md lg:max-w-none mx-auto animate-float"
          style="perspective: 1200px;" 
          @mousemove="handleImageMouseMove"
          @mouseleave="handleImageMouseLeave"
        >
          <div class="relative group aspect-[4/3] sm:aspect-square lg:aspect-[4/5] xl:aspect-[3/4] overflow-hidden rounded-2xl sm:rounded-3xl">
            <div class="absolute -inset-3 sm:-inset-4 bg-gradient-to-tr from-indigo-200 via-sky-100 to-violet-100 rounded-2xl sm:rounded-3xl blur-xl opacity-50 group-hover:opacity-75 transition-opacity duration-500 z-0"></div>
            
            <img 
              src="/superteam.png" 
              alt="Desk Setup Visual Identity" 
              class="relative w-full h-full object-cover rounded-2xl sm:rounded-3xl shadow-xl border border-slate-200/60 bg-white transition-transform duration-200 ease-out z-10"
              :style="{ transform: imageTransform }"
            />

            <div class="absolute inset-0 z-20 pointer-events-none mix-blend-screen opacity-0 group-hover:opacity-100 transition-opacity duration-300 animate-shimmer"></div>
          </div>
        </div>

      </div>
    </div>
  </section>
</template>

<style scoped>
/* Background Blobs Animation */
@keyframes blob-animation {
  0% { transform: translate(0px, 0px) scale(1); }
  33% { transform: translate(20px, -30px) scale(1.05); }
  66% { transform: translate(-15px, 20px) scale(0.98); }
  100% { transform: translate(0px, 0px) scale(1); }
}

.animate-blob {
  animation: blob-animation 12s infinite ease-in-out;
}
.animation-delay-2000 {
  animation-delay: 2s;
}
.animation-delay-4000 {
  animation-delay: 4s;
}

/* Image Floating Animation */
@keyframes float-dynamic {
  0%, 100% {
    transform: translateY(0px) rotate(0deg);
  }
  50% {
    transform: translateY(-10px) rotate(0.5deg);
  }
}

.animate-float {
  animation: float-dynamic 6s infinite ease-in-out;
}

/* Sharp, High-Visibility Metallic Shimmer Sweep */
@keyframes shimmer-sweep {
  0% {
    background: linear-gradient(
      110deg, 
      rgba(255, 255, 255, 0) 30%, 
      rgba(255, 255, 255, 0.55) 45%, 
      rgba(255, 255, 255, 0.85) 50%, 
      rgba(255, 255, 255, 0.55) 55%, 
      rgba(255, 255, 255, 0) 70%
    );
    background-size: 250% 100%;
    background-position: 160% 0;
  }
  100% {
    background: linear-gradient(
      110deg, 
      rgba(255, 255, 255, 0) 30%, 
      rgba(255, 255, 255, 0.55) 45%, 
      rgba(255, 255, 255, 0.85) 50%, 
      rgba(255, 255, 255, 0.55) 55%, 
      rgba(255, 255, 255, 0) 70%
    );
    background-size: 250% 100%;
    background-position: -60% 0;
  }
}

.animate-shimmer {
  /* Sped up from 2.5s to 1.8s for a snappier, more striking flash */
  animation: shimmer-sweep 1.8s infinite cubic-bezier(0.4, 0, 0.2, 1);
}
</style>