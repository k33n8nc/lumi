<script setup>
import { onMounted, ref } from 'vue'
import gsap from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'

// Register GSAP plugins on client-side
if (process.client) {
  gsap.registerPlugin(ScrollTrigger)
}

useHead({
  title: 'Lumi | Helder in Kinderopvang',
  meta: [
    { name: 'description', content: 'Lumi Support staat naast kinderopvangorganisaties die rust, overzicht en continuïteit zoeken.' }
  ]
})

// Team members with diverse roles to replace duplicates
const team = [
  { name: 'Ailko Treebusch', role: 'Eigenaar & Oprichter', icon: '👤' },
  { name: 'Linda de Vries', role: 'Senior Planner', icon: '👩‍💼' },
  { name: 'Mark de Jong', role: 'Financieel Specialist', icon: '👨‍💼' },
  { name: 'Annelies Bakker', role: 'Debiteurenbeheer', icon: '👩‍💻' }
]

// Method to programmatic scroll on CTA click
const scrollToExpertises = () => {
  if (process.client) {
    const container = document.querySelector('#morph-container')
    if (container) {
      const scrollPos = container.offsetTop + (window.innerHeight * 0.8)
      window.scrollTo({
        top: scrollPos,
        behavior: 'smooth'
      })
    }
  }
}

onMounted(() => {
  if (process.client) {
    // Single pinned morphing timeline combining Hero and Expertises
    const morphTl = gsap.timeline({
      scrollTrigger: {
        trigger: '#morph-container',
        start: 'top top',
        end: '+=130%', // Scroll distance to complete the morph transition
        scrub: true,
        pin: true,
        invalidateOnRefresh: true
      }
    })

    // Step 1: Hero content fades out and translates upwards
    morphTl.to('.hero-content', {
      opacity: 0,
      y: -80,
      duration: 0.3
    }, 0)
    .to('.hero-scroll-prompt', {
      opacity: 0,
      y: -20,
      duration: 0.2
    }, 0)

    // Step 2: Background shifts to white and Sunrise circle expands in center
    .to('#morph-container', {
      backgroundColor: '#ffffff',
      duration: 0.5
    }, 0.15)
    .to('.sunrise-circle', {
      scale: 1,
      opacity: 1,
      duration: 0.5,
      ease: 'power1.out'
    }, 0.15)

    // Step 3: Navigation theme transitions from white to dark blue
    .to('.nav-logo-text', {
      color: '#0c2440',
      duration: 0.4
    }, 0.2)
    .to('.nav-logo-img', {
      filter: 'invert(13%) sepia(30%) saturate(2220%) hue-rotate(193deg) brightness(92%) contrast(97%)', // maps white to #0c2440
      duration: 0.4
    }, 0.2)
    .to('.nav-contact-btn', {
      color: '#0c2440',
      borderColor: 'rgba(12, 36, 64, 0.2)',
      duration: 0.4
    }, 0.2)

    // Step 4: Expertises content slides in from below and fades in
    .fromTo('.expertises-layer', 
      { opacity: 0, y: 60 },
      {
        opacity: 1,
        y: 0,
        duration: 0.4,
        ease: 'power2.out',
        onStart: () => {
          const el = document.querySelector('.expertises-layer')
          if (el) el.style.pointerEvents = 'auto'
          const hl = document.querySelector('.hero-content')
          if (hl) hl.style.pointerEvents = 'none'
        },
        onReverseComplete: () => {
          const el = document.querySelector('.expertises-layer')
          if (el) el.style.pointerEvents = 'none'
          const hl = document.querySelector('.hero-content')
          if (hl) hl.style.pointerEvents = 'auto'
        }
      },
      0.45
    )

    // ScrollTrigger entrance animation for Team section
    gsap.fromTo('.team-card',
      { opacity: 0, scale: 0.93, y: 20 },
      {
        opacity: 1,
        scale: 1,
        y: 0,
        stagger: 0.08,
        duration: 0.6,
        scrollTrigger: {
          trigger: '#team',
          start: 'top 75%',
          toggleActions: 'play none none none'
        }
      }
    )
  }
})
</script>

<template>
  <div class="min-h-screen text-white selection:bg-lumi-yellow selection:text-lumi-blue-dark relative overflow-x-hidden">
    
    <!-- Wrapper -->
    <div id="scroll-wrapper" class="relative">
      
      <!-- Combined Morph Container (Pins Hero and morphs into Expertises) -->
      <section id="morph-container" class="w-full h-screen bg-lumi-blue-dark relative overflow-hidden flex flex-col justify-between items-center px-6 py-12">
        
        <!-- Background Hero Glow Layer (fades out as sunrise starts) -->
        <div class="absolute inset-0 bg-[radial-gradient(circle_at_center,rgba(29,70,117,0.15)_0%,transparent_70%)] pointer-events-none hero-bg-glow"></div>

        <!-- The Sunrise Circle (expands behind the cards) -->
        <div class="sunrise-circle absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 w-[700px] h-[700px] md:w-[900px] md:h-[900px] rounded-full bg-lumi-yellow pointer-events-none scale-0 opacity-0 z-0"></div>

        <!-- Navigation Bar (Stays on screen but shifts colors) -->
        <div class="w-full max-w-7xl flex justify-between items-center h-16 relative z-30">
          <div class="flex items-center gap-3">
            <div class="flex items-center justify-center p-1 bg-white/5 border border-white/10 rounded-lg">
              <img src="~/assets/images/logo.png" alt="Lumi" class="h-6 w-auto filter invert brightness-200 nav-logo-img" />
            </div>
            <div class="flex flex-col text-left">
              <span class="font-bold text-sm tracking-tight text-white nav-logo-text">LUMI</span>
              <span class="text-[8px] font-semibold tracking-wider text-zinc-400 uppercase">Helder in kinderopvang</span>
            </div>
          </div>
          <a 
            href="mailto:info@lumi-support.nl" 
            class="border border-white/20 hover:border-lumi-yellow hover:text-lumi-yellow px-4 py-2 rounded-xl text-xs tracking-wider font-semibold transition-colors uppercase nav-contact-btn"
          >
            CONTACT
          </a>
        </div>

        <!-- Hero Content Layer -->
        <div class="max-w-4xl my-auto space-y-8 relative z-20 py-12 hero-content">
          <h1 class="text-4xl sm:text-5xl lg:text-7xl font-extrabold tracking-tight leading-[1.15]">
            Lumi brengt <span class="bg-gradient-to-r from-lumi-yellow via-amber-300 to-white bg-clip-text text-transparent">helderheid</span> in uw organisatie.
          </h1>
          <p class="text-zinc-300 text-base sm:text-lg max-w-2xl mx-auto leading-relaxed font-medium">
            Lumi Support staat naast kinderopvangorganisaties die rust, overzicht en continuïteit zoeken. Met jarenlange praktijkervaring binnen de kinderopvang weten wij precies waar de uitdagingen liggen — van planning en oudercommunicatie tot facturatie en debiteurenbeheer.
          </p>
          <div class="pt-4">
            <button 
              @click="scrollToExpertises"
              class="inline-block bg-lumi-yellow hover:bg-lumi-yellow-hover text-lumi-blue-dark font-extrabold px-10 py-4.5 rounded-full shadow-lg shadow-lumi-yellow/10 transition-all hover:scale-105 active:scale-95 text-xs tracking-wider cursor-pointer"
            >
              PLAN KENNISMAKING
            </button>
          </div>
        </div>

        <!-- Expertises Layer (fades/slides in on top of sunrise) -->
        <div class="expertises-layer absolute inset-0 flex flex-col justify-center items-center px-6 py-12 opacity-0 pointer-events-none z-10">
          <div class="w-full max-w-6xl mt-10">
            
            <!-- Heading -->
            <div class="mb-12 text-left">
              <h2 class="text-4xl sm:text-5xl font-extrabold tracking-tight relative inline-block text-lumi-blue-dark">
                Onze expertises
                <span class="absolute bottom-[-10px] left-0 w-24 h-1.5 bg-lumi-blue-dark rounded-full"></span>
              </h2>
            </div>

            <!-- 6 clean empty cards as requested -->
            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
              <div 
                v-for="i in 6" 
                :key="i" 
                class="bg-[#e5e7eb]/70 border border-zinc-200/40 rounded-2xl p-8 h-52 transition-all duration-300 hover:shadow-xl hover:-translate-y-1"
              >
                <!-- Empty placeholder rectangle as requested -->
              </div>
            </div>

          </div>
        </div>

        <!-- Scroll prompt -->
        <div class="text-zinc-400 text-[10px] tracking-[0.2em] uppercase relative z-20 animate-bounce hero-scroll-prompt">
          Scroll voor verheldering
          <div class="text-base mt-1">↓</div>
        </div>

      </section>

      <!-- Section 3: Lumi Team (Yellow Background, matching 03_team) -->
      <section id="team" class="min-h-screen bg-lumi-yellow text-lumi-blue-dark py-28 px-6 flex flex-col justify-center items-center relative overflow-hidden">
        
        <!-- Faded Pattern Layer -->
        <div class="absolute inset-0 bg-black/5 opacity-[0.03] pointer-events-none"></div>

        <div class="w-full max-w-6xl relative z-10 space-y-16">
          
          <!-- Section Heading -->
          <div class="text-left">
            <h2 class="text-4xl sm:text-5xl font-extrabold tracking-tight relative inline-block text-lumi-blue">
              Lumi team
              <span class="absolute bottom-[-10px] left-0 w-24 h-1.5 bg-white rounded-full"></span>
            </h2>
          </div>

          <!-- Team Cards Grid -->
          <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-8">
            <div 
              v-for="(member, index) in team" 
              :key="index" 
              class="team-card bg-white/20 hover:bg-white/30 border border-white/35 rounded-2xl p-6 flex items-center gap-4 transition-all duration-300 hover:shadow-lg"
            >
              <!-- Avatar Circle Placeholder -->
              <div class="w-14 h-14 rounded-full bg-white flex-shrink-0 shadow-sm flex items-center justify-center text-xl font-bold text-lumi-blue">
                {{ member.icon }}
              </div>
              <div class="text-left">
                <h4 class="font-extrabold text-base text-lumi-blue">{{ member.name }}</h4>
                <span class="text-xs font-semibold text-lumi-blue-bright/70 block mt-0.5">{{ member.role }}</span>
              </div>
            </div>
          </div>

          <!-- Call to Action bottom button -->
          <div class="pt-8 text-center sm:text-left">
            <a 
              href="mailto:info@lumi-support.nl"
              class="inline-block bg-lumi-blue hover:bg-lumi-blue-dark text-white font-extrabold px-10 py-4.5 rounded-full shadow-lg transition-all hover:scale-105 active:scale-95 text-xs tracking-wider"
            >
              ADMINISTRATIE EXPERTS
            </a>
          </div>

        </div>
      </section>

      <!-- Minimal Dark Blue Footer -->
      <footer class="bg-lumi-blue-dark text-zinc-400 py-12 px-6 border-t border-white/5 text-center text-xs tracking-wider">
        <div class="max-w-7xl mx-auto flex flex-col sm:flex-row justify-between items-center gap-6">
          <div class="flex items-center gap-3">
            <div class="flex items-center justify-center p-1 bg-white/5 border border-white/10 rounded-lg">
              <img src="~/assets/images/logo.png" alt="Lumi" class="h-5 w-auto filter invert brightness-200" />
            </div>
            <span class="font-bold text-sm tracking-tight text-white">LUMI</span>
          </div>
          <div>
            Contact: <a href="mailto:info@lumi-support.nl" class="text-white hover:text-lumi-yellow underline">info@lumi-support.nl</a>
          </div>
          <div>
            &copy; 2026 Lumi Support. Alle rechten voorbehouden.
          </div>
        </div>
      </footer>

    </div>
  </div>
</template>

<style scoped>
/* Scoped styles for high-performance transitions */
.sunrise-circle {
  will-change: transform, opacity;
}
.hero-content, .hero-scroll-prompt {
  will-change: opacity, transform;
}
.expertises-layer {
  will-change: opacity, transform;
}
</style>
