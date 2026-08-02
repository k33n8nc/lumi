<script setup lang="ts">
import { ref } from 'vue'
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'
import { faArrowTrendUp, faHandshake, faHeart } from '@fortawesome/free-solid-svg-icons'

const sectionRef = ref<HTMLElement | null>(null)

const careerValues = [
  {
    icon: faHandshake,
    title: 'Flexibiliteit & vertrouwen',
    text: 'Vrijheid om je werk goed in te richten, met duidelijke afspraken en vertrouwen als basis.'
  },
  {
    icon: faArrowTrendUp,
    title: 'Persoonlijke groei',
    text: 'Ruimte om te leren, initiatief te nemen en samen onze dienstverlening steeds beter te maken.'
  },
  {
    icon: faHeart,
    title: 'Werk met betekenis',
    text: 'Met jouw aandacht help je kinderopvang-organisaties iedere dag vooruit.'
  }
]

const scrollToCareers = () => {
  if (!sectionRef.value) return
  sectionRef.value.scrollIntoView({ behavior: 'smooth' })
}

defineExpose({
  scrollToCareers
})
</script>

<template>
  <section
    id="werken-bij"
    ref="sectionRef"
    class="w-full py-24 px-6 md:px-16 bg-white text-lumi-navy border-t border-slate-100"
    aria-labelledby="careers-title"
  >
    <div class="w-full max-w-[100rem] mx-auto flex flex-col gap-16">
      <!-- Careers Intro -->
      <div class="flex flex-col gap-4 max-w-3xl">
        <span class="text-xs uppercase tracking-widest text-lumi-gold-text font-bold">
          Werken bij Lumi
        </span>
        <h1 id="careers-title">
          Rust in je werk.<br>Ruimte om te groeien.
        </h1>
        <p class="text-body-lg text-slate-700 leading-relaxed mt-2">
          Bij Lumi Support geloven we dat rust en betrokkenheid hand in hand gaan. We zoeken mensen
          die zorgvuldig werken, graag meedenken en zich thuis voelen in de wereld van kinderopvang.
        </p>
      </div>

      <!-- Career Values Grid -->
      <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
        <article
          v-for="value in careerValues"
          :key="value.title"
          class="flex flex-col p-8 rounded-3xl bg-slate-50 border border-slate-100 hover:shadow-lg transition-all duration-200 gap-4"
        >
          <span class="inline-grid place-items-center w-14 h-14 rounded-2xl bg-lumi-gold-bg text-lumi-gold-text text-2xl" aria-hidden="true">
            <FontAwesomeIcon :icon="value.icon" />
          </span>
          <h3 class="text-xl font-bold text-lumi-navy mt-2">
            {{ value.title }}
          </h3>
          <p class="text-slate-600 text-body-md leading-relaxed">
            {{ value.text }}
          </p>
        </article>
      </div>
    </div>
  </section>
</template>
