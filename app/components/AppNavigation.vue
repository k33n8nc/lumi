<script setup lang="ts">
import { ref } from 'vue'

const emit = defineEmits<{
  (e: 'navigate', sectionId: string): void
}>()

const menuOpen = ref(false)

const handleNavigate = (sectionId: string) => {
  menuOpen.value = false
  emit('navigate', sectionId)
}
</script>

<template>
  <div>
    <!-- Hamburger Button -->
    <button
      class="menu-button"
      type="button"
      :aria-expanded="menuOpen"
      aria-label="Menu openen"
      @click="menuOpen = !menuOpen"
    >
      <span />
      <span />
      <span />
    </button>

    <!-- Overlay Menu Panel -->
    <Transition
      enter-active-class="transition-opacity duration-300 ease-out"
      enter-from-class="opacity-0"
      enter-to-class="opacity-100"
      leave-active-class="transition-opacity duration-200 ease-in"
      leave-from-class="opacity-100"
      leave-to-class="opacity-0"
    >
      <nav
        v-if="menuOpen"
        class="fixed inset-0 z-[90] flex flex-col items-center justify-center px-6 py-12 bg-lumi-navy overflow-hidden select-none"
        aria-label="Hoofdnavigatie"
      >
        <!-- LOGO WITH SUBTLE LIGHT EFFECT -->
        <div class="relative flex flex-col items-center mb-6 sm:mb-8">
          <!-- SUBTLE ROUNDED LIGHT BEAM (LUMI YELLOW) -->
          <div class="pointer-events-none absolute -top-4 sm:-top-6 left-1/2 -translate-x-1/2 w-[620px] sm:w-[780px] md:w-[900px] h-[550px] sm:h-[650px] md:h-[750px] -z-10 select-none overflow-visible" aria-hidden="true">
            <svg
              class="w-full h-full overflow-visible"
              viewBox="0 0 800 600"
              fill="none"
              xmlns="http://www.w3.org/2000/svg"
            >
              <defs>
                <!-- Subtle Lumi Yellow Gradient -->
                <linearGradient id="lumiNavBeam" x1="400" y1="20" x2="400" y2="600" gradientUnits="userSpaceOnUse">
                  <stop offset="0%" stop-color="#ffd24a" stop-opacity="0.22" />
                  <stop offset="30%" stop-color="#ffd24a" stop-opacity="0.12" />
                  <stop offset="65%" stop-color="#ffd24a" stop-opacity="0.04" />
                  <stop offset="100%" stop-color="#ffd24a" stop-opacity="0" />
                </linearGradient>

                <!-- Soft Gaussian Blur Filter -->
                <filter id="navSubtleGlow" x="-20%" y="-20%" width="140%" height="140%">
                  <feGaussianBlur stdDeviation="16" />
                </filter>
              </defs>

              <!-- Rounded dome top expanding into smooth light cone -->
              <path
                d="M 355 70 C 355 20, 445 20, 445 70 L 740 590 C 740 590, 400 600, 60 590 Z"
                fill="url(#lumiNavBeam)"
                filter="url(#navSubtleGlow)"
              />
            </svg>

            <!-- Soft ambient glow right behind the bulb -->
            <div class="absolute top-2 left-1/2 -translate-x-1/2 -translate-y-1/4 w-[160px] h-[160px] rounded-full bg-[radial-gradient(circle,rgba(255,210,74,0.25)_0%,rgba(255,210,74,0.08)_45%,transparent_70%)] blur-[18px]" />
          </div>

          <!-- LOGO IMAGE (WITTE VARIANT) -->
          <div class="relative">
            <img
              src="~/assets/images/logo-trans-wit.png"
              alt="Lumi Logo"
              class="relative z-10 w-16 h-auto sm:w-20 md:w-22 select-none drop-shadow-[0_0_16px_rgba(255,210,74,0.45)]"
            />
          </div>
        </div>

        <!-- Navigation Links (Centered) -->
        <div class="relative z-10 flex flex-col items-center gap-3 sm:gap-4 md:gap-5">
          <button
            type="button"
            class="p-0 bg-transparent border-0 text-white hover:text-lumi-yellow text-3xl sm:text-5xl md:text-6xl font-bold tracking-tight transition-colors text-center cursor-pointer"
            @click="handleNavigate('hero')"
          >
            Home
          </button>
          <button
            type="button"
            class="p-0 bg-transparent border-0 text-white hover:text-lumi-yellow text-3xl sm:text-5xl md:text-6xl font-bold tracking-tight transition-colors text-center cursor-pointer"
            @click="handleNavigate('visie')"
          >
            Hier geloven wij in
          </button>
          <button
            type="button"
            class="p-0 bg-transparent border-0 text-white hover:text-lumi-yellow text-3xl sm:text-5xl md:text-6xl font-bold tracking-tight transition-colors text-center cursor-pointer"
            @click="handleNavigate('diensten')"
          >
            Onze diensten
          </button>
          <button
            type="button"
            class="p-0 bg-transparent border-0 text-white hover:text-lumi-yellow text-3xl sm:text-5xl md:text-6xl font-bold tracking-tight transition-colors text-center cursor-pointer"
            @click="handleNavigate('team')"
          >
            Ons team
          </button>
          <button
            type="button"
            class="p-0 bg-transparent border-0 text-white hover:text-lumi-yellow text-3xl sm:text-5xl md:text-6xl font-bold tracking-tight transition-colors text-center cursor-pointer"
            @click="handleNavigate('contact')"
          >
            Kennismaken
          </button>
        </div>
      </nav>
    </Transition>
  </div>
</template>

<style scoped>
.menu-button {
  position: fixed;
  z-index: 99;
  top: clamp(2rem, 5vh, 3.2rem);
  right: clamp(1.5rem, 4vw, 4.5rem);
  display: flex;
  width: 3.5rem;
  height: 2.75rem;
  padding: 0.35rem;
  border: 0;
  background: transparent;
  cursor: pointer;
  flex-direction: column;
  justify-content: space-between;
  mix-blend-mode: difference;
}

.menu-button span {
  display: block;
  width: 100%;
  height: 0.24rem;
  background: white;
  transition: transform 220ms ease, opacity 180ms ease;
}

.menu-button[aria-expanded='true'] span:first-child {
  transform: translateY(0.9rem) rotate(45deg);
}

.menu-button[aria-expanded='true'] span:nth-child(2) {
  opacity: 0;
}

.menu-button[aria-expanded='true'] span:last-child {
  transform: translateY(-0.9rem) rotate(-45deg);
}
</style>
