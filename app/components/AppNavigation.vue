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
        class="fixed inset-0 z-[90] flex flex-col items-start justify-center px-8 md:px-24 py-20 bg-lumi-navy/98 gap-4"
        aria-label="Hoofdnavigatie"
      >
        <button
          type="button"
          class="p-0 bg-transparent border-0 text-white hover:text-lumi-yellow text-4xl sm:text-5xl md:text-7xl font-bold tracking-tight transition-colors text-left cursor-pointer"
          @click="handleNavigate('hero')"
        >
          Home
        </button>
        <button
          type="button"
          class="p-0 bg-transparent border-0 text-white hover:text-lumi-yellow text-4xl sm:text-5xl md:text-7xl font-bold tracking-tight transition-colors text-left cursor-pointer"
          @click="handleNavigate('diensten')"
        >
          Onze diensten
        </button>
        <button
          type="button"
          class="p-0 bg-transparent border-0 text-white hover:text-lumi-yellow text-4xl sm:text-5xl md:text-7xl font-bold tracking-tight transition-colors text-left cursor-pointer"
          @click="handleNavigate('team')"
        >
          Ons team
        </button>
        <button
          type="button"
          class="p-0 bg-transparent border-0 text-white hover:text-lumi-yellow text-4xl sm:text-5xl md:text-7xl font-bold tracking-tight transition-colors text-left cursor-pointer"
          @click="handleNavigate('contact')"
        >
          Kennismaken
        </button>
        <button
          type="button"
          class="p-0 bg-transparent border-0 text-white hover:text-lumi-yellow text-4xl sm:text-5xl md:text-7xl font-bold tracking-tight transition-colors text-left cursor-pointer"
          @click="handleNavigate('werken-bij')"
        >
          Werken bij
        </button>
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
