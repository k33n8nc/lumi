<script setup lang="ts">
const emit = defineEmits<{
  (e: 'scrollToServices'): void
}>()

const handleScrollToServices = () => {
  emit('scrollToServices')
}
</script>

<template>
  <section
    id="hero"
    class="relative w-full h-screen min-h-[42rem] flex flex-col justify-center items-center overflow-hidden bg-lumi-navy text-lumi-white px-6 py-20 md:py-16 select-none"
    aria-label="Introductie"
  >
    <div class="relative z-10 max-w-[62rem] text-center flex flex-col items-center">
      
      <!-- LOGO WITH SUBTLE LIGHT EFFECT -->
      <div class="relative flex flex-col items-center">
        <!-- SUBTLE ROUNDED LIGHT BEAM (LUMI YELLOW) -->
        <div class="pointer-events-none absolute -top-4 sm:-top-6 left-1/2 -translate-x-1/2 w-[620px] sm:w-[820px] md:w-[980px] h-[500px] sm:h-[580px] md:h-[650px] -z-10 select-none overflow-visible" aria-hidden="true">
          <svg
            class="w-full h-full overflow-visible"
            viewBox="0 0 800 600"
            fill="none"
            xmlns="http://www.w3.org/2000/svg"
          >
            <defs>
              <!-- Subtle Lumi Yellow Gradient -->
              <linearGradient id="lumiSubtleBeam" x1="400" y1="20" x2="400" y2="600" gradientUnits="userSpaceOnUse">
                <stop offset="0%" stop-color="#ffd24a" stop-opacity="0.22" />
                <stop offset="30%" stop-color="#ffd24a" stop-opacity="0.12" />
                <stop offset="65%" stop-color="#ffd24a" stop-opacity="0.04" />
                <stop offset="100%" stop-color="#ffd24a" stop-opacity="0" />
              </linearGradient>

              <!-- Soft Gaussian Blur Filter -->
              <filter id="subtleGlow" x="-20%" y="-20%" width="140%" height="140%">
                <feGaussianBlur stdDeviation="16" />
              </filter>
            </defs>

            <!-- Rounded dome top expanding into smooth light cone -->
            <path
              d="M 355 70 C 355 20, 445 20, 445 70 L 740 590 C 740 590, 400 600, 60 590 Z"
              fill="url(#lumiSubtleBeam)"
              filter="url(#subtleGlow)"
            />
          </svg>

          <!-- Soft ambient glow right behind the bulb -->
          <div class="absolute top-2 left-1/2 -translate-x-1/2 -translate-y-1/4 w-[180px] h-[180px] rounded-full bg-[radial-gradient(circle,rgba(255,210,74,0.25)_0%,rgba(255,210,74,0.08)_45%,transparent_70%)] blur-[18px]" />
        </div>

        <!-- LOGO IMAGE -->
        <div class="relative mb-5 md:mb-6">
          <img
            src="~/assets/images/logo-trans-kleur-wit.png"
            alt="Lumi Logo"
            class="relative z-10 w-16 h-auto sm:w-20 md:w-22 select-none drop-shadow-[0_0_16px_rgba(255,210,74,0.45)]"
          />
        </div>
      </div>

      <h1>
        Lumi brengt <em class="text-lumi-yellow not-italic">helderheid</em><br>in uw organisatie.
      </h1>
      <p class="max-w-[42rem] mx-auto mt-6 text-slate-200 text-body-lg">
        Lumi Support staat naast kinderopvangorganisaties die rust, overzicht en continuïteit zoeken.
        Met jarenlange praktijkervaring binnen de kinderopvang weten wij precies waar de uitdagingen
        liggen - van planning en oudercommunicatie tot facturatie en debiteurenbeheer.
      </p>
      <button
        class="inline-flex items-center justify-center min-w-[18rem] mt-8 px-8 py-3.5 border-0 rounded-full bg-lumi-yellow text-lumi-navy font-extrabold text-sm tracking-wider uppercase cursor-pointer hover:-translate-y-0.5 hover:bg-[#ffdc6f] transition-all duration-180"
        type="button"
        @click="handleScrollToServices"
      >
        Hier geloven wij in...
      </button>
    </div>
  </section>
</template>
