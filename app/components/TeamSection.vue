<script setup lang="ts">
import { ref } from 'vue'
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'
import { faHeart, faUsers } from '@fortawesome/free-solid-svg-icons'
import { ScrollSmoother } from 'gsap/ScrollSmoother'
import peopleGroupImg from '~/assets/images/peoplegroup.webp'

const sectionRef = ref<HTMLElement | null>(null)

const scrollToTeam = () => {
  if (!sectionRef.value) return
  const smoother = ScrollSmoother.get()
  if (smoother) {
    smoother.scrollTo(sectionRef.value, true)
  } else {
    sectionRef.value.scrollIntoView({ behavior: 'smooth' })
  }
}

defineExpose({
  scrollToTeam
})
</script>

<template>
  <section
    id="ons-team"
    ref="sectionRef"
    class="relative w-full min-h-screen flex flex-col justify-center py-20 md:py-28 px-6 md:px-16 bg-white text-lumi-navy border-t border-slate-100 overflow-hidden"
    aria-label="Ons team"
  >
    <div class="w-full max-w-[100rem] mx-auto grid grid-cols-1 lg:grid-cols-12 gap-12 lg:gap-16 items-center">
      
      <!-- Left Column: Copy & Story -->
      <div class="lg:col-span-6 flex flex-col gap-6">
        <h1 class="text-lumi-navy">
          Het team achter<br><em class="text-lumi-yellow not-italic">Lumi</em> Support
        </h1>
        <div class="flex flex-col gap-5 text-slate-700 text-body-lg leading-relaxed mt-2">
          <p>
            Onze persoonlijke aanpak maakt het verschil. Wij zijn een hecht en betrokken team met een grote focus op uw kwaliteit, continuïteit en rust.
          </p>
          <p>
            Met jarenlange praktijkervaring binnen kinderopvangorganisaties begrijpen we de dagelijkse dynamiek als geen ander. Samen zorgen we voor overzicht en zekerheid in uw administratie.
          </p>
        </div>

        <!-- Team Highlights / Micro Badges -->
        <!-- <div class="grid grid-cols-1 sm:grid-cols-2 gap-4 pt-2">
          <div class="flex items-center gap-3.5 p-4 rounded-xl bg-slate-50 border border-slate-100">
            <span class="inline-grid place-items-center w-10 h-10 rounded-full bg-lumi-gold-bg text-lumi-gold-text text-base flex-shrink-0" aria-hidden="true">
              <FontAwesomeIcon :icon="faUsers" />
            </span>
            <div class="flex flex-col">
              <span class="text-sm font-bold text-lumi-navy">Vaste contactpersonen</span>
              <span class="text-xs text-slate-500">Korte lijnen & direct contact</span>
            </div>
          </div>

          <div class="flex items-center gap-3.5 p-4 rounded-xl bg-slate-50 border border-slate-100">
            <span class="inline-grid place-items-center w-10 h-10 rounded-full bg-lumi-gold-bg text-lumi-gold-text text-base flex-shrink-0" aria-hidden="true">
              <FontAwesomeIcon :icon="faHeart" />
            </span>
            <div class="flex flex-col">
              <span class="text-sm font-bold text-lumi-navy">100% Betrokkenheid</span>
              <span class="text-xs text-slate-500">Oog voor uw organisatie</span>
            </div>
          </div>
        </div> -->
      </div>

      <!-- Right Column: Framed Group Photo -->
      <div class="lg:col-span-6 flex items-center justify-center lg:justify-end">
        <div class="relative w-full max-w-[38rem] group">
          <!-- Background decorative aura -->
          <div
            class="absolute -inset-2 rounded-[2rem] bg-gradient-to-tr from-lumi-yellow/35 via-amber-100/50 to-transparent blur-xl opacity-70 -z-10 group-hover:opacity-100 transition-opacity duration-300"
            aria-hidden="true"
          />

          <!-- Photo Container -->
          <div class="relative overflow-hidden rounded-[1.75rem] border border-slate-200/90 shadow-xl bg-slate-100 aspect-[4/3] sm:aspect-[16/11]">
            <img
              :src="peopleGroupImg"
              alt="Het team van Lumi Support"
              class="w-full h-full object-cover object-center group-hover:scale-103 transition-transform duration-500 ease-out"
            />
          </div>
        </div>
      </div>

    </div>
  </section>
</template>
