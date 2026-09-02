<script setup lang="ts">
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'
import { faEnvelope, faLocationDot, faPhone } from '@fortawesome/free-solid-svg-icons'
import logoImg from '~/assets/images/logo.png'

const emit = defineEmits<{
  (e: 'navigate', sectionId: string): void
}>()
</script>

<template>
  <footer class="w-full bg-lumi-navy text-white pt-20 pb-10 px-6 md:px-16 border-t border-white/10" aria-label="Voetnavigatie">
    <div class="w-full max-w-[100rem] mx-auto flex flex-col gap-16">
      <!-- Main Footer Grid -->
      <div class="grid grid-cols-1 lg:grid-cols-12 gap-12 items-start">
        <!-- Logo & Tagline (Left) -->
        <div class="lg:col-span-6 flex flex-col items-start gap-4">
          <img
            :src="logoImg"
            alt="Lumi Support Logo"
            class="w-28 sm:w-36 md:w-40 h-auto -translate-x-6 sm:-translate-x-8 md:-translate-x-10"
          >
          <!-- <p class="text-body-lg text-slate-300 max-w-md leading-relaxed">
            Administratieve rust voor de kinderopvang.
          </p> -->
        </div>

        <!-- Navigation & Contact Columns (Right) -->
        <div class="lg:col-span-6 grid grid-cols-1 sm:grid-cols-2 gap-10">
          <!-- Nav Links -->
          <nav class="flex flex-col gap-4" aria-label="Footernavigatie links">
            <h3 class="text-sm uppercase tracking-wider text-lumi-yellow font-bold">
              Navigatie
            </h3>
            <div class="flex flex-col gap-3">
              <button
                type="button"
                class="text-left text-slate-300 hover:text-white transition-colors text-base cursor-pointer bg-transparent border-0 p-0"
                @click="emit('navigate', 'hero')"
              >
                Home
              </button>
              <button
                type="button"
                class="text-left text-slate-300 hover:text-white transition-colors text-base cursor-pointer bg-transparent border-0 p-0"
                @click="emit('navigate', 'visie')"
              >
                Hier geloven wij in
              </button>
              <button
                type="button"
                class="text-left text-slate-300 hover:text-white transition-colors text-base cursor-pointer bg-transparent border-0 p-0"
                @click="emit('navigate', 'diensten')"
              >
                Onze diensten
              </button>
              <button
                type="button"
                class="text-left text-slate-300 hover:text-white transition-colors text-base cursor-pointer bg-transparent border-0 p-0"
                @click="emit('navigate', 'team')"
              >
                Ons team
              </button>
              <button
                type="button"
                class="text-left text-slate-300 hover:text-white transition-colors text-base cursor-pointer bg-transparent border-0 p-0"
                @click="emit('navigate', 'contact')"
              >
                Kennismaken
              </button>
            </div>
          </nav>

          <!-- Contact Details -->
          <div class="flex flex-col gap-4">
            <h3 class="text-sm uppercase tracking-wider text-lumi-yellow font-bold">
              Contact
            </h3>
            <div class="flex flex-col gap-4">
              <a
                href="mailto:contact@lumi-support.nl"
                class="flex items-center gap-3 text-slate-300 hover:text-white transition-colors group no-underline text-base"
              >
                <span class="inline-grid place-items-center w-8 h-8 rounded-full bg-white/10 text-lumi-yellow group-hover:bg-lumi-yellow group-hover:text-lumi-navy transition-all" aria-hidden="true">
                  <FontAwesomeIcon :icon="faEnvelope" />
                </span>
                <span>contact@lumi-support.nl</span>
              </a>

              <a
                href="tel:+31640937499"
                class="flex items-center gap-3 text-slate-300 hover:text-white transition-colors group no-underline text-base"
              >
                <span class="inline-grid place-items-center w-8 h-8 rounded-full bg-white/10 text-lumi-yellow group-hover:bg-lumi-yellow group-hover:text-lumi-navy transition-all" aria-hidden="true">
                  <FontAwesomeIcon :icon="faPhone" />
                </span>
                <span>+31 (0)6 409 37 499</span>
              </a>

              <div class="flex items-center gap-3 text-slate-300 text-base">
                <span class="inline-grid place-items-center w-8 h-8 rounded-full bg-white/10 text-lumi-yellow" aria-hidden="true">
                  <FontAwesomeIcon :icon="faLocationDot" />
                </span>
                <span>Landelijk werkzaam</span>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- Bottom Bar -->
      <div class="flex flex-col sm:flex-row justify-between items-center pt-8 border-t border-white/10 text-xs text-slate-400 gap-4">
        <span>© 2026 Lumi Support B.V. All rights reserved.</span>
        <div class="flex items-center gap-6">
          <span class="hover:text-slate-200 cursor-pointer">Privacybeleid</span>
          <span class="hover:text-slate-200 cursor-pointer">Voorwaarden</span>
        </div>
      </div>
    </div>
  </footer>
</template>
