<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const scrollToTop = () => {
  window.scrollTo({ top: 0, behavior: 'smooth' })
}

// References for interactive background animation
const canvasRef = ref(null)
let animationFrameId = null

onMounted(() => {
  const canvas = canvasRef.value
  if (!canvas) return
  const ctx = canvas.getContext('2d')
  
  let particles = []
  const maxParticles = 60 // Controls density of drifting nodes
  const mouse = { x: null, y: null, radius: 160 } // Interaction zone size

  // Track cursor position only relative to the canvas section bounding box
  const handleMouseMove = (e) => {
    const rect = canvas.getBoundingClientRect()
    mouse.x = e.clientX - rect.left
    mouse.y = e.clientY - rect.top
  }

  const handleMouseLeave = () => {
    mouse.x = null
    mouse.y = null
  }

  // Handle responsiveness on viewport size adjustments
  const resizeCanvas = () => {
    if (canvas.parentElement) {
      canvas.width = canvas.parentElement.offsetWidth
      canvas.height = canvas.parentElement.offsetHeight
    }
  }
  
  window.addEventListener('resize', resizeCanvas)
  canvas.parentElement.addEventListener('mousemove', handleMouseMove)
  canvas.parentElement.addEventListener('mouseleave', handleMouseLeave)
  resizeCanvas()

  // Particle Blueprint
  class Particle {
    constructor() {
      this.x = Math.random() * canvas.width
      this.y = Math.random() * canvas.height
      this.vx = (Math.random() - 0.5) * 0.4 // Slow speed for tranquility look
      this.vy = (Math.random() - 0.5) * 0.4
      this.radius = Math.random() * 2 + 1.5
    }

    update() {
      this.x += this.vx
      this.y += this.vy

      // Bounce properties off canvas layout bounds
      if (this.x < 0 || this.x > canvas.width) this.vx = -this.vx
      if (this.y < 0 || this.y > canvas.height) this.vy = -this.vy

      // Mouse magnet pull interaction logic
      if (mouse.x !== null && mouse.y !== null) {
        const dx = mouse.x - this.x
        const dy = mouse.y - this.y
        const distance = Math.sqrt(dx * dx + dy * dy)
        if (distance < mouse.radius) {
          const force = (mouse.radius - distance) / mouse.radius
          this.x -= (dx / distance) * force * 0.6
          this.y -= (dy / distance) * force * 0.6
        }
      }
    }

    draw() {
      ctx.beginPath()
      ctx.arc(this.x, this.y, this.radius, 0, Math.PI * 2)
      // Soft indigo tint matching theme palette
      ctx.fillStyle = 'rgba(99, 102, 241, 0.25)' 
      ctx.fill()
    }
  }

  // Populate node array loop
  for (let i = 0; i < maxParticles; i++) {
    particles.push(new Particle())
  }

  // Render Frame Loop
  const animate = () => {
    ctx.clearRect(0, 0, canvas.width, canvas.height)
    
    // Draw connections between overlapping node proximities
    for (let i = 0; i < particles.length; i++) {
      particles[i].update()
      particles[i].draw()
      
      for (let j = i + 1; j < particles.length; j++) {
        const dx = particles[i].x - particles[j].x
        const dy = particles[i].y - particles[j].y
        const dist = Math.sqrt(dx * dx + dy * dy)
        
        if (dist < 110) {
          ctx.beginPath()
          ctx.moveTo(particles[i].x, particles[i].y)
          ctx.lineTo(particles[j].x, particles[j].y)
          // Dynamic alpha styling based on proximity distance link
          ctx.strokeStyle = `rgba(99, 102, 241, ${0.12 * (1 - dist / 110)})`
          ctx.lineWidth = 0.8
          ctx.stroke()
        }
      }
    }
    animationFrameId = requestAnimationFrame(animate)
  }
  
  animate()

  // Clean memory leaks on navigation unmounting
  onUnmounted(() => {
    window.removeEventListener('resize', resizeCanvas)
    if (canvas.parentElement) {
      canvas.parentElement.removeEventListener('mousemove', handleMouseMove)
      canvas.parentElement.removeEventListener('mouseleave', handleMouseLeave)
    }
    cancelAnimationFrame(animationFrameId)
  })
})
</script>

<template>
  <section id="contact" class="py-16 sm:py-24 bg-gradient-to-b from-slate-50 to-white relative overflow-hidden">
    
    <canvas 
      ref="canvasRef" 
      class="absolute top-0 left-0 w-full h-full pointer-events-none z-0"
    ></canvas>

    <div class="absolute top-0 right-0 w-1/2 h-full bg-gradient-to-l from-indigo-500/[0.02] to-transparent pointer-events-none z-0"></div>

    <div class="max-w-7xl mx-auto px-4 sm:px-6 relative z-10">
      
      <div class="text-left max-w-4xl mb-12 sm:mb-16">
        <div class="inline-flex items-center gap-2 bg-indigo-50 px-3 py-1 rounded-full border border-indigo-100/80 mb-4">
          <span class="w-1.5 h-1.5 rounded-full bg-indigo-600"></span>
          <p class="text-indigo-600 font-black text-[10px] uppercase tracking-widest">Get In Touch</p>
        </div>
        
        <h2 class="text-3xl sm:text-4xl md:text-5xl font-black text-slate-900 tracking-tight leading-tight mb-4 sm:mb-6">
          Let's create something meaningful together
        </h2>
        
        <p class="text-sm sm:text-base md:text-lg text-slate-600 max-w-3xl font-light leading-relaxed">
          We're a team of student developers from CvSU Naic dedicated to building digital solutions that make a difference. Whether you need a website, web application, or technical consultation, we're here to help bring your ideas to life with clean code and thoughtful design.
        </p>
      </div>

      <div class="flex flex-col sm:flex-row gap-4 items-start sm:items-center mb-16 sm:mb-24">
        
        <a 
          href="mailto:triotagapayo@gmail.com"
          class="w-full sm:w-auto bg-white/80 backdrop-blur-md border border-slate-200/60 rounded-2xl shadow-xl shadow-slate-100/40 px-6 py-4 flex items-center gap-4 hover:shadow-2xl hover:shadow-indigo-100/30 hover:border-indigo-300/80 transition-all duration-300 transform hover:-translate-y-0.5 group"
        >
          <div class="w-10 h-10 rounded-xl bg-indigo-50 flex items-center justify-center text-indigo-600 group-hover:bg-indigo-600 group-hover:text-white transition-colors duration-300">
            <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z"></path>
            </svg>
          </div>
          <div class="flex flex-col text-left">
            <span class="text-[10px] font-black uppercase text-slate-400 tracking-wider">Email Us</span>
            <span class="text-slate-800 text-sm font-bold tracking-wide">triotagapayo@gmail.com</span>
          </div>
        </a>
        
        <div class="w-full sm:w-auto bg-white/80 backdrop-blur-md border border-slate-200/60 rounded-2xl shadow-xl shadow-slate-100/40 px-6 py-4 flex items-center gap-4 transition-all duration-300">
          <div class="w-10 h-10 rounded-xl bg-slate-50 flex items-center justify-center text-slate-500">
            <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z"></path>
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 11a3 3 0 11-6 0 3 3 0 016 0z"></path>
            </svg>
          </div>
          <div class="flex flex-col text-left">
            <span class="text-[10px] font-black uppercase text-slate-400 tracking-wider">Location</span>
            <span class="text-slate-700 text-sm font-bold tracking-wide">Naic, Cavite, Philippines</span>
          </div>
        </div>

      </div>

      <footer class="border-t border-slate-200/80 pt-8 sm:pt-10">
        <div class="flex flex-col-reverse md:flex-row justify-between items-start md:items-center gap-6 md:gap-4">
          
          <p class="text-slate-400 font-mono text-[10px] sm:text-xs tracking-wider uppercase">
            © 2026 TRIOTAGAPAYO. DESIGNED FOR TRANQUILITY.
          </p>
          
          <div class="flex flex-wrap gap-x-8 gap-y-2 text-xs sm:text-sm font-medium text-slate-500">
            <a href="#" class="hover:text-indigo-600 transition-colors">Privacy Policy</a>
            <a href="#" class="hover:text-indigo-600 transition-colors">Terms of Service</a>
            <a href="#" class="hover:text-indigo-600 transition-colors">Social</a>
          </div>
          
          <button 
            @click="scrollToTop"
            aria-label="Scroll to top"
            class="self-end md:self-auto w-10 h-10 sm:w-12 sm:h-12 bg-slate-50 hover:bg-indigo-600 text-slate-600 hover:text-white rounded-xl flex items-center justify-center transition-all duration-300 cursor-pointer border border-slate-200/60 hover:border-indigo-600 shadow-md shadow-slate-100/80 hover:-translate-y-1"
          >
            <svg class="w-5 h-5 transform group-hover:scale-110 transition-transform" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 10l7-7m0 0l7 7m-7-7v18"></path>
            </svg>
          </button>

        </div>
      </footer>
    </div>
  </section>
</template>