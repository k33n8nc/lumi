<script setup lang="ts">
import { ref } from 'vue'
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'
import {
  faAward,
  faCircleCheck,
  faLightbulb,
  faRotate
} from '@fortawesome/free-solid-svg-icons'
import { ScrollSmoother } from 'gsap/ScrollSmoother'

const sectionRef = ref<HTMLElement | null>(null)

const beliefs = [
  {
    icon: faRotate,
    title: 'Continuïteit',
    text: 'Jullie administratie staat nooit stil. Bij ziekte, vakantie of personeelswisselingen zorgen wij ervoor dat het werk gewoon doorgaat.'
  },
  {
    icon: faCircleCheck,
    title: '100% kwaliteit',
    text: 'Jullie moeten erop kunnen vertrouwen dat de administratie en facturatie kloppen. Daarom werken we zorgvuldig, gestructureerd en met vaste controles.'
  },
  {
    icon: faAward,
    title: 'Deskundigheid',
    text: 'Wij kennen de kinderopvang én de systemen en processen erachter. Daardoor voeren we niet alleen uit, maar denken we met jullie mee en zien we waar het slimmer of beter kan.'
  }
]

const scrollToBeliefs = () => {
  if (!sectionRef.value) return
  const smoother = ScrollSmoother.get()
  if (smoother) {
    smoother.scrollTo(sectionRef.value, true)
  } else {
    sectionRef.value.scrollIntoView({ behavior: 'smooth' })
  }
}

defineExpose({
  scrollToBeliefs
})
</script>

<template>
  <section
    id="visie"
    ref="sectionRef"
    class="relative w-full min-h-screen flex flex-col justify-center py-20 md:py-28 px-6 md:px-16 bg-white text-lumi-navy border-t border-slate-100"
    aria-labelledby="beliefs-title"
  >
    <div class="w-full max-w-[100rem] mx-auto flex flex-col gap-14 md:gap-16">
      
      <!-- Top Grid: Intro Copy on Left, Pillars on Right -->
      <div class="grid grid-cols-1 lg:grid-cols-12 gap-12 lg:gap-20 xl:gap-24 items-start">
        
        <!-- Left Column: Heading, Story Paragraphs & Concluding Quote -->
        <div class="lg:col-span-6 flex flex-col gap-6">
          <h1 id="beliefs-title" class="text-lumi-navy/90">
            Hier geloven wij in
          </h1>
          <div class="flex flex-col gap-5 text-lumi-navy/90 text-body-lg leading-relaxed mt-2">
            <p>
              Wij geloven dat kinderopvang draait om kinderen, niet om administratie. Kinderopvangorganisaties verdienen de ruimte om zich te richten op wat écht belangrijk is: het bieden van liefdevolle en kwalitatieve opvang. Daarom nemen wij administratieve processen uit handen en zorgen we voor rust, overzicht en continuïteit.
            </p>
            <p>
              Met onze jarenlange ervaring in de kinderopvang en diepgaande kennis van Jaamo combineren we praktijkkennis met slimme processen. We voeren niet alleen uit, maar denken mee, signaleren kansen en helpen organisaties hun administratie steeds slimmer en efficiënter in te richten.
            </p>

            <!-- Concluding Quote Statement -->
            <blockquote class="relative pl-5 border-l-2 border-lumi-yellow text-lumi-navy/50 italic font-medium text-body-lg leading-relaxed pt-1 pb-1 mt-2">
              &ldquo;Zo zorgen wij voor rust, zekerheid en grip op jullie administratie, zodat jullie je kunnen richten op waar het écht om draait: <span class="text-lumi-yellow">de kinderen</span>.&rdquo;
            </blockquote>
          </div>
        </div>

        <!-- Right Column: 3 Vertical Value Pillars (Equal Height) -->
        <div class="lg:col-span-6 grid grid-cols-1 auto-rows-fr gap-5">
          <article
            v-for="belief in beliefs"
            :key="belief.title"
            class="flex flex-col sm:flex-row items-start h-full p-6 sm:p-7 rounded-2xl bg-lumi-yellow hover:shadow-md transition-shadow duration-200 gap-4 sm:gap-5"
          >
            <span class="inline-grid place-items-center w-12 h-12 rounded-full bg-lumi-navy/10 text-lumi-navy text-xl flex-shrink-0 shadow-sm" aria-hidden="true">
              <FontAwesomeIcon :icon="belief.icon" />
            </span>
            <div class="flex flex-col gap-1.5">
              <h3 class="text-lumi-navy">
                {{ belief.title }}
              </h3>
              <p class="text-lumi-navy/80 text-body-md leading-relaxed">
                {{ belief.text }}
              </p>
            </div>
          </article>
        </div>
      </div>
    </div>
  </section>
</template>
