<script setup>
const skills = [
  { name: 'Figma', icon: '🎨' },
  { name: 'PHP', icon: '🐘' },
  { name: 'CSS3', icon: '🎨' },
  { name: 'JavaScript', icon: '🌐' },
  { name: 'Java', icon: '☕' },
  { name: 'HTML', icon: '📄' }
]

const achievements = [
  {
    title: "President's Lister",
    description: "Recognized as a President's Lister for the first semester, achieving a General Weighted Average (GWA) of 1.33 through rigorous coursework and technical projects",
    gwa: '1.33',
    image: 'dreipres.jpg', 
    tags: ['ACADEMIC', 'HONORS']
  },
  {
    title: "Dean's Lister (Academic Scholar)",
    description: "Maintained high academic standing for the 1st Sem A.Y. 2024-2025, earning the status of Partial Academic Scholar with a GWA of 1.51",
    gwa: '1.51',
    image: 'dreidean.jpg',
    tags: ['ACADEMIC', 'HONORS']
  }
]

// Reusable smooth scroll utility
const scrollToSection = (id) => {
  const element = document.getElementById(id);
  if (element) {
    element.scrollIntoView({ behavior: 'smooth' });
  }
}
</script>

<template>
  <section id="andrei-profile" class="py-10 md:py-20 bg-transparent">
    <div class="max-w-7xl mx-auto px-4 sm:px-6">
      
      <div class="bg-white/80 backdrop-blur-md rounded-3xl p-5 sm:p-10 lg:p-14 mb-12 max-w-7xl mx-auto border border-slate-200/60 shadow-xl shadow-slate-100/50 transition-all duration-500 hover:shadow-2xl hover:shadow-indigo-100/40">
        
        <div class="flex flex-col lg:flex-row lg:items-center gap-6 sm:gap-10 lg:gap-16">
          
          <div class="flex items-center lg:items-start gap-4 sm:gap-6 lg:gap-0 lg:contents">
            
            <div class="w-20 h-20 sm:w-32 sm:h-32 lg:w-auto lg:h-auto lg:flex-1 lg:max-w-[420px] order-1 lg:order-2 relative group/image flex-shrink-0">
              <div class="hidden lg:block absolute top-0 -left-4 w-64 h-64 bg-indigo-200 rounded-full mix-blend-multiply filter blur-2xl opacity-30 group-hover/image:opacity-50 transition-opacity duration-700 animate-blob"></div>
              <div class="hidden lg:block absolute -bottom-4 -right-4 w-64 h-64 bg-sky-200 rounded-full mix-blend-multiply filter blur-2xl opacity-30 group-hover/image:opacity-50 transition-opacity duration-700 animate-blob animation-delay-2000"></div>
              
              <div class="relative overflow-hidden rounded-2xl lg:rounded-3xl border border-slate-200 bg-white p-1 sm:p-2 lg:p-3 shadow-md lg:shadow-xl transition-all duration-500 group-hover/image:scale-[1.02] group-hover/image:shadow-2xl">
                <img 
                  src="/dreiteam.jpg" 
                  alt="John Andrei P. Manguera"
                  class="w-full h-full lg:h-[460px] object-cover rounded-xl lg:rounded-2xl filter contrast-[1.02] group-hover/image:scale-105 transition-transform duration-700 ease-out"
                />
                <div class="absolute inset-1 sm:inset-2 lg:inset-3 bg-gradient-to-t from-slate-950/20 via-transparent to-transparent opacity-0 group-hover/image:opacity-100 transition-opacity duration-500 rounded-xl lg:rounded-2xl pointer-events-none"></div>
              </div>
            </div>

            <div class="flex-1 lg:hidden order-2">
              <div class="inline-flex items-center gap-1.5 bg-indigo-50 px-2.5 py-0.5 rounded-full border border-indigo-100/80 mb-1.5">
                <span class="w-1 h-1 rounded-full bg-indigo-600"></span>
                <p class="text-indigo-600 font-black text-[9px] uppercase tracking-widest">Front-end Dev</p>
              </div>
              <h2 class="text-xl sm:text-3xl font-black text-slate-900 tracking-tight leading-tight">
                John Andrei P. Manguera
              </h2>
            </div>

          </div>

          <div class="lg:flex-1 space-y-5 sm:space-y-6 order-3 lg:order-1 text-left">
            <div class="hidden lg:inline-flex items-center gap-2 bg-indigo-50 px-3 py-1 rounded-full border border-indigo-100/80 animate-pulse">
              <span class="w-1.5 h-1.5 rounded-full bg-indigo-600"></span>
              <p class="text-indigo-600 font-black text-[10px] uppercase tracking-widest">
                Front-end Developer
              </p>
            </div>
            
            <h2 class="hidden lg:block text-4xl lg:text-5xl font-black text-slate-900 tracking-tight leading-tight">
              John Andrei P. Manguera
            </h2>
            
            <p class="text-slate-600 leading-relaxed text-sm sm:text-base font-light">
              Hi, I'm Andrei! I'm a student developer currently grinding my way through a degree. I specialize in building the 'front-facing' world of the web, focusing on turning complex ideas into clean, interactive interfaces. I treat my code like a high-performance game engine—optimizing every line for speed and responsiveness to ensure a 'zero-lag' user experience.
            </p>
            
            <div class="group/quote border-l-4 border-indigo-600 pl-4 sm:pl-5 py-3 sm:py-4 bg-gradient-to-r from-indigo-50/60 to-transparent rounded-r-2xl transition-all duration-300 hover:from-indigo-50 hover:pl-6">
              <p class="text-slate-700 italic text-sm sm:text-base leading-relaxed font-normal transition-colors group-hover/quote:text-indigo-950">
                "Every great interface starts with a tutorial; my goal is to make the user's journey feel like a legendary speedrun."
              </p>
            </div>

            <div class="flex flex-col sm:flex-row gap-3 sm:gap-4 pt-1 sm:pt-2">
              <button 
                @click="scrollToSection('andrei-skills')"
                class="w-full sm:w-auto relative overflow-hidden group/btn bg-indigo-600 text-white px-7 py-3.5 sm:px-8 sm:py-4 rounded-xl transition-all duration-300 font-bold text-xs sm:text-sm tracking-wider cursor-pointer shadow-md shadow-indigo-600/10 hover:shadow-lg hover:shadow-indigo-600/30 hover:-translate-y-0.5"
              >
                <span class="absolute inset-0 w-full h-full bg-gradient-to-r from-indigo-700 to-violet-700 opacity-0 group-hover/btn:opacity-100 transition-opacity duration-300"></span>
                <span class="relative flex items-center justify-center gap-2">
                  VIEW SKILLS <span class="transform group-hover/btn:translate-x-1 transition-transform">→</span>
                </span>
              </button>
              
              <button 
                @click="scrollToSection('andrei-achievements')"
                class="w-full sm:w-auto group/btn2 bg-slate-50 text-slate-700 hover:text-indigo-600 px-7 py-3.5 sm:px-8 sm:py-4 rounded-xl transition-all duration-300 font-bold text-xs sm:text-sm tracking-wider cursor-pointer border border-slate-200 hover:border-indigo-300 hover:bg-indigo-50/30 hover:-translate-y-0.5"
              >
                <span class="flex items-center justify-center gap-2">
                  ACHIEVEMENTS <span class="transform group-hover/btn2:translate-y-0.5 transition-transform">↓</span>
                </span>
              </button>
            </div>
          </div>

        </div>
      </div>

    </div>

    <div id="andrei-skills" class="mb-12 sm:mb-20 py-16 sm:py-20 bg-slate-100/50 left-1/2 right-1/2 -ml-[50vw] -mr-[50vw] w-screen relative scroll-mt-24 overflow-hidden border-y border-slate-200/40">
      <h3 class="text-2xl sm:text-3xl font-black text-slate-900 mb-2 sm:mb-3 text-center tracking-tight">Expertise & Tools</h3>
      <p class="text-xs sm:text-base text-slate-500 mb-10 sm:mb-12 text-center max-w-2xl mx-auto px-4 font-light">
        We leverage a modern stack to build interfaces that are fast, accessible, and future-proof.
      </p>
      
      <div class="w-full relative overflow-x-hidden [mask-image:linear-gradient(to_right,transparent,white_10%,white_90%,transparent)]">
        <div class="flex gap-4 sm:gap-6 w-max animate-marquee hover:[animation-play-state:paused]">
          
          <div 
            v-for="(skill, index) in skills" 
            :key="'andrei-set1-' + index"
            class="bg-white rounded-2xl p-5 sm:p-6 text-center border border-slate-200/50 shadow-xs w-[180px] sm:w-[220px] flex-shrink-0 flex flex-col items-center justify-center gap-2 sm:gap-3 group"
          >
            <div class="text-3xl sm:text-4xl filter grayscale opacity-85 group-hover:grayscale-0 transition-all duration-300">{{ skill.icon }}</div>
            <p class="font-bold text-slate-800 text-xs sm:text-sm tracking-wide">{{ skill.name }}</p>
          </div>

          <div 
            v-for="(skill, index) in skills" 
            :key="'andrei-set2-' + index"
            class="bg-white rounded-2xl p-5 sm:p-6 text-center border border-slate-200/50 shadow-xs w-[180px] sm:w-[220px] flex-shrink-0 flex flex-col items-center justify-center gap-2 sm:gap-3 group"
          >
            <div class="text-3xl sm:text-4xl filter grayscale opacity-85 group-hover:grayscale-0 transition-all duration-300">{{ skill.icon }}</div>
            <p class="font-bold text-slate-800 text-xs sm:text-sm tracking-wide">{{ skill.name }}</p>
          </div>

        </div>
      </div>
    </div>

    <div id="andrei-achievements" class="py-12 sm:py-20 bg-transparent scroll-mt-24">
      <div class="max-w-7xl mx-auto px-4 sm:px-6">
        <h3 class="text-2xl sm:text-3xl font-black text-slate-900 mb-2 text-center tracking-tight">Achievements</h3>
        <p class="text-sm sm:text-base text-slate-500 mb-12 text-center max-w-2xl mx-auto font-light">
          A showcase of academic excellence and commitment to the field of Information Technology.
        </p>
        
        <div class="flex flex-col gap-6 max-w-5xl mx-auto md:grid md:grid-cols-2 md:gap-12">
          <div 
            v-for="(achievement, index) in achievements" 
            :key="index"
            class="group flex flex-row items-start md:flex-col gap-4 sm:gap-6 bg-white md:bg-transparent p-4 sm:p-5 rounded-2xl border border-slate-100 md:border-0 md:p-0 shadow-xs md:shadow-none transition-all duration-300"
          >
            <div class="w-24 h-24 sm:w-32 sm:h-32 md:w-full md:h-auto md:aspect-[4/3] rounded-xl sm:rounded-2xl overflow-hidden shadow-sm border border-slate-200/60 relative bg-slate-50 flex-shrink-0">
              <img 
                :src="achievement.image" 
                :alt="achievement.title"
                class="w-full h-full object-cover transition-transform duration-700 ease-out group-hover:scale-[1.04]"
              />
              <div class="absolute inset-0 bg-slate-950/15 opacity-0 group-hover:opacity-100 transition-opacity duration-300 pointer-events-none"></div>
              
              <div class="hidden sm:block absolute bottom-3 left-3 sm:bottom-4 sm:left-4 bg-white/90 backdrop-blur-md text-slate-900 font-mono text-[10px] sm:text-xs font-black px-2.5 py-1 sm:px-3 sm:py-1.5 rounded-xl shadow-xs border border-white/40">
                ★ GWA {{ achievement.gwa }}
              </div>
            </div>

            <div class="space-y-1 sm:space-y-2 flex-1 pt-1 md:pt-0">
              <div class="sm:hidden text-indigo-600 font-mono text-[10px] font-black tracking-wide mb-0.5">
                ★ GWA {{ achievement.gwa }}
              </div>
              
              <h4 class="text-sm sm:text-base md:text-lg font-bold text-slate-900 group-hover:text-indigo-600 transition-colors duration-300 tracking-tight leading-tight">
                {{ achievement.title }}
              </h4>
              
              <p class="text-slate-500 text-[11px] sm:text-xs leading-relaxed font-light line-clamp-3 md:line-clamp-none">
                {{ achievement.description }}
              </p>

              <div class="hidden sm:flex flex-wrap gap-3 pt-1">
                <span 
                  v-for="(tag, tagIndex) in achievement.tags" 
                  :key="tagIndex"
                  class="text-indigo-600 font-bold text-[9px] sm:text-[10px] uppercase tracking-widest"
                >
                  // {{ tag }}
                </span>
              </div>
            </div>

          </div>
        </div>
      </div>
    </div>

  </section>
</template>

<style scoped>
@keyframes marquee-horizontal {
  0% { transform: translateX(0%); }
  100% { transform: translateX(-50%); }
}

.animate-marquee {
  animation: marquee-horizontal 20s linear infinite;
}
</style>