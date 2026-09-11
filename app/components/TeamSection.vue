<script setup lang="ts">
import { ref } from 'vue'
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'
import { faUser } from '@fortawesome/free-solid-svg-icons'

const sectionRef = ref<HTMLElement | null>(null)

const teamMembers = [
  {
    name: 'Stanley Husen',
    role: 'Eigenaar & Oprichter',
    image: '/images/stanley.jpg'
  },
  {
    name: 'Ailko Treebusch',
    role: 'Eigenaar & Oprichter',
    image: '/images/ailko.jpg'
  },
  {
    name: 'Patricia Danckaerts',
    role: 'Operationeel Manager',
    image: '/images/patricia.jpg'
  }
]

const scrollToTeam = () => {
  sectionRef.value?.scrollIntoView({ behavior: 'smooth' })
}

defineExpose({
  scrollToTeam
})
</script>

<template>
  <section
    id="ons-team"
    ref="sectionRef"
    class="relative w-full min-h-screen flex flex-col justify-center py-20 md:py-28 px-6 md:px-16 bg-white text-lumi-navy border-t border-slate-100"
    aria-labelledby="team-title"
  >
    <div class="w-full max-w-[100rem] mx-auto flex flex-col">
      
      <!-- Section Header -->
      <header class="text-center mb-10 md:mb-14">
        <h1 id="team-title" class="text-lumi-navy">
          Het <span class="text-lumi-yellow">lumi</span> team
        </h1>
        <div class="max-w-2xl mx-auto mt-4">
          <blockquote class="relative border-b-2 border-lumi-yellow text-lumi-navy/60 italic font-medium text-body-lg leading-relaxed pb-6">
            &ldquo;Onze persoonlijke aanpak maakt het verschil. Wij zijn een hecht en betrokken team met een grote focus op jullie kwaliteit, continuïteit en rust.&rdquo;
          </blockquote>
        </div>
      </header>

      <!-- 3 Team Member Cards Grid (Matching reference mockup) -->
      <div class="grid grid-cols-1 md:grid-cols-3 gap-8 md:gap-6 lg:gap-8 max-w-sm sm:max-w-md md:max-w-5xl mx-auto w-full px-6 sm:px-10 md:px-0">
        <article
          v-for="member in teamMembers"
          :key="member.name"
          class="group flex flex-col items-center text-center p-5 sm:p-6 rounded-2xl bg-lumi-yellow border border-amber-300/40 shadow-sm hover:shadow-xl hover:shadow-amber-500/10 transition-all duration-300"
        >
          <!-- Photo Placeholder -->
          <div class="relative w-full aspect-[4/5] rounded-xl overflow-hidden bg-white/60 mb-5 flex items-center justify-center border border-white/80 group-hover:scale-[1.02] transition-transform duration-300">
            <img
              v-if="member.image"
              :src="member.image"
              :alt="member.name"
              class="w-full h-full object-cover object-center"
            />
            <span v-else class="text-4xl sm:text-5xl text-lumi-navy/25 group-hover:text-lumi-navy/50 transition-colors">
              <FontAwesomeIcon :icon="faUser" />
            </span>
          </div>

          <!-- Name & Role -->
          <h3 class="text-lumi-navy font-bold text-lg sm:text-xl">
            {{ member.name }}
          </h3>
          <p class="text-lumi-navy/70 text-body-md font-medium mt-1">
            {{ member.role }}
          </p>
        </article>
      </div>

    </div>
  </section>
</template>
