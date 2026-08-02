<script setup lang="ts">
import { nextTick, onBeforeUnmount, onMounted, ref } from 'vue'
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'
import { faEnvelope, faPhone } from '@fortawesome/free-solid-svg-icons'
import gsap from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'

const sectionRef = ref<HTMLElement | null>(null)

const formSubmitted = ref(false)
const formState = ref({
  name: '',
  email: '',
  message: ''
})

const handleSubmit = () => {
  formSubmitted.value = true
  console.log('Form submitted:', formState.value)
}

let animationContext: gsap.Context | null = null

const scrollToTeam = () => {
  if (!sectionRef.value) return
  const trigger = ScrollTrigger.getById('team-contact-transition')
  const target = trigger ? trigger.start : sectionRef.value.offsetTop
  window.scrollTo({ top: target, behavior: 'smooth' })
}

const scrollToContact = () => {
  if (!sectionRef.value) return
  const trigger = ScrollTrigger.getById('team-contact-transition')
  const target = trigger
    ? trigger.start + (trigger.end - trigger.start) * 0.85
    : sectionRef.value.offsetTop + window.innerHeight
  window.scrollTo({ top: target, behavior: 'smooth' })
}

defineExpose({
  scrollToTeam,
  scrollToContact
})

onMounted(async () => {
  gsap.registerPlugin(ScrollTrigger)
  await nextTick()

  const prefersReducedMotion = window.matchMedia('(prefers-reduced-motion: reduce)').matches

  if (prefersReducedMotion) {
    gsap.set('.team-panel', { opacity: 1, visibility: 'visible' })
    gsap.set('.contact-panel', { opacity: 1, visibility: 'visible' })
    return
  }

  animationContext = gsap.context(() => {
    const timeline = gsap.timeline({
      defaults: { ease: 'none' },
      scrollTrigger: {
        id: 'team-contact-transition',
        trigger: sectionRef.value,
        start: 'top top',
        end: '+=200%',
        scrub: 0.8,
        pin: true,
        anticipatePin: 1,
        invalidateOnRefresh: true
      }
    })

    timeline
      // Phase 1: Team copy slides up & fades out
      .to('.team-copy', { opacity: 0, yPercent: -15, duration: 0.3 }, 0)
      // Team visual box morphs/translates down
      .to('.team-visual-box', { opacity: 0, scale: 0.9, yPercent: 20, duration: 0.35 }, 0.08)
      // Phase 2: Contact panel reveals and slides up into place vertically
      .set('.contact-panel', { visibility: 'visible' }, 0.32)
      .fromTo(
        '.contact-panel',
        { opacity: 0, yPercent: 35 },
        { opacity: 1, yPercent: 0, duration: 0.48 },
        0.35
      )
  }, sectionRef.value ?? undefined)

  ScrollTrigger.refresh()
})

onBeforeUnmount(() => {
  animationContext?.revert()
})
</script>

<template>
  <section
    ref="sectionRef"
    class="relative w-full h-[100svh] min-h-[42rem] overflow-hidden isolation-isolate bg-white text-lumi-navy"
    aria-label="Team en kennismaken"
  >
    <!-- TEAM STAGE (Starts visible) -->
    <div
      id="ons-team"
      class="team-panel absolute inset-0 z-[1] flex items-center justify-center px-6 md:px-16 py-16 text-lumi-navy will-change-transform"
    >
      <div class="w-full max-w-[100rem] mx-auto grid grid-cols-1 lg:grid-cols-12 gap-10 lg:gap-16 items-center">
        <!-- Team Text Content -->
        <div class="team-copy lg:col-span-5 flex flex-col gap-6">
          <h2>
            Het team achter<br><em class="text-lumi-yellow not-italic">Lumi</em> Support
          </h2>
          <p class="text-body-lg text-slate-700 leading-relaxed">
            Onze persoonlijke aanpak maakt het verschil. Wij zijn een klein team met een grote focus
            op uw kwaliteit en rust.
          </p>
        </div>

        <!-- Team Visual Box -->
        <div class="lg:col-span-7">
          <div class="team-visual-box relative w-full h-[300px] sm:h-[400px] lg:h-[480px] rounded-[2.5rem] bg-lumi-yellow shadow-xl flex items-center justify-center overflow-hidden">
            <span class="text-3xl sm:text-5xl md:text-6xl font-extrabold text-lumi-navy/25 tracking-tight">
              Team Lumi
            </span>
          </div>
        </div>
      </div>
    </div>

    <!-- CONTACT STAGE (Slides up vertically on scroll scrub) -->
    <div
      id="kennismaken"
      class="contact-panel absolute inset-0 z-[2] invisible opacity-0 flex items-center justify-center px-6 md:px-16 py-16 text-lumi-navy will-change-transform"
    >
      <div class="w-full max-w-[100rem] mx-auto">
        <div class="grid grid-cols-1 lg:grid-cols-12 rounded-[2.5rem] overflow-hidden shadow-2xl">
          <!-- Left: Contact Info Card -->
          <div class="lg:col-span-6 bg-lumi-navy text-white p-8 sm:p-12 lg:p-14 flex flex-col justify-between gap-8">
            <div>
              <h2 class="text-white">
                Laten we kennismaken
              </h2>
              <p class="mt-4 text-body-lg text-slate-300 leading-relaxed max-w-xl">
                Wilt u weten wat Lumi Support voor uw kinderopvangorganisatie kan betekenen?
                Neem vandaag nog contact met ons op.
              </p>
            </div>

            <div class="flex flex-col gap-5">
              <!-- Mail Option -->
              <a
                href="mailto:contact@lumi-support.nl"
                class="flex items-center gap-4 text-white hover:text-lumi-yellow transition-colors group no-underline"
              >
                <span class="inline-grid place-items-center w-12 h-12 rounded-full bg-lumi-yellow text-lumi-navy text-lg group-hover:scale-105 transition-transform" aria-hidden="true">
                  <FontAwesomeIcon :icon="faEnvelope" />
                </span>
                <div class="flex flex-col">
                  <span class="text-xs uppercase tracking-wider text-slate-400 font-bold">Mail ons</span>
                  <span class="text-base sm:text-lg font-medium">contact@lumi-support.nl</span>
                </div>
              </a>

              <!-- Phone Option -->
              <a
                href="tel:+31640937499"
                class="flex items-center gap-4 text-white hover:text-lumi-yellow transition-colors group no-underline"
              >
                <span class="inline-grid place-items-center w-12 h-12 rounded-full bg-lumi-yellow text-lumi-navy text-lg group-hover:scale-105 transition-transform" aria-hidden="true">
                  <FontAwesomeIcon :icon="faPhone" />
                </span>
                <div class="flex flex-col">
                  <span class="text-xs uppercase tracking-wider text-slate-400 font-bold">Bel ons</span>
                  <span class="text-base sm:text-lg font-medium">+31 (0)6 40937499</span>
                </div>
              </a>
            </div>
          </div>

          <!-- Right: Contact Form Card -->
          <div class="lg:col-span-6 bg-[#263f5d] text-white p-8 sm:p-12 lg:p-14 flex flex-col justify-center">
            <div v-if="formSubmitted" class="p-8 bg-emerald-500/20 border border-emerald-400/30 rounded-2xl text-center flex flex-col items-center gap-3">
              <h3 class="text-white text-2xl font-bold">Bedankt!</h3>
              <p class="text-slate-200">Uw bericht is succesvol verzonden. Wij nemen zo snel mogelijk contact met u op.</p>
              <button
                type="button"
                class="mt-4 px-6 py-2 bg-lumi-yellow text-lumi-navy font-bold rounded-xl text-sm uppercase"
                @click="formSubmitted = false"
              >
                Nieuw bericht
              </button>
            </div>

            <form v-else class="flex flex-col gap-5" @submit.prevent="handleSubmit">
              <div class="flex flex-col gap-2">
                <label for="name" class="text-xs uppercase tracking-wider text-slate-300 font-bold">Naam</label>
                <input
                  id="name"
                  v-model="formState.name"
                  type="text"
                  name="name"
                  autocomplete="name"
                  required
                  class="w-full h-12 px-4 rounded-xl bg-[#50657c] border border-[#74869a] text-white focus:outline-none focus:border-lumi-yellow focus:ring-2 focus:ring-lumi-yellow/30 transition-all"
                >
              </div>

              <div class="flex flex-col gap-2">
                <label for="email" class="text-xs uppercase tracking-wider text-slate-300 font-bold">E-mailadres</label>
                <input
                  id="email"
                  v-model="formState.email"
                  type="email"
                  name="email"
                  autocomplete="email"
                  required
                  class="w-full h-12 px-4 rounded-xl bg-[#50657c] border border-[#74869a] text-white focus:outline-none focus:border-lumi-yellow focus:ring-2 focus:ring-lumi-yellow/30 transition-all"
                >
              </div>

              <div class="flex flex-col gap-2">
                <label for="message" class="text-xs uppercase tracking-wider text-slate-300 font-bold">Bericht</label>
                <textarea
                  id="message"
                  v-model="formState.message"
                  name="message"
                  rows="3"
                  required
                  class="w-full p-4 rounded-xl bg-[#50657c] border border-[#74869a] text-white focus:outline-none focus:border-lumi-yellow focus:ring-2 focus:ring-lumi-yellow/30 transition-all resize-y"
                />
              </div>

              <button
                type="submit"
                class="w-full h-13 mt-2 bg-lumi-yellow text-lumi-navy font-bold text-sm uppercase tracking-wider rounded-xl cursor-pointer hover:bg-[#ffdc6f] hover:-translate-y-0.5 transition-all duration-180"
              >
                Verstuur bericht
              </button>
            </form>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
