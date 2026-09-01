<script setup lang="ts">
import { nextTick, onBeforeUnmount, onMounted, ref } from 'vue'
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'
import {
  faCalendarDays,
  faFileInvoiceDollar,
  faFileSignature,
  faLaptopCode,
  faLightbulb,
  faListCheck,
  faMoneyCheckDollar,
  faUserPlus
} from '@fortawesome/free-solid-svg-icons'
import gsap from 'gsap'
import { ScrollSmoother } from 'gsap/ScrollSmoother'
import { ScrollTrigger } from 'gsap/ScrollTrigger'

const transitionSection = ref<HTMLElement | null>(null)
const servicesTrack = ref<HTMLElement | null>(null)

const services = [
  {
    id: 'inschrijvingen',
    icon: faUserPlus,
    title: ['Inschrijvingen &', 'Oudercommunicatie'],
    text: 'Wij verzorgen het volledige inschrijfproces en onderhouden toegankelijke communicatie via e-mail en telefoon.'
  },
  {
    id: 'planning',
    icon: faCalendarDays,
    title: ['Planning &', 'Groepsbezetting'],
    text: 'Optimale planning van kinderen en groepen voor een gezonde bezettingsgraad en efficiënte inzet.'
  },
  {
    id: 'wachtlijstbeheer',
    icon: faListCheck,
    title: ['Professioneel', 'wachtlijstbeheer'],
    text: 'Professioneel beheer van wachtlijsten op basis van uw specifieke prioriteiten en regels.'
  },
  {
    id: 'contracten',
    icon: faFileSignature,
    title: ['Opvolgen digitale', 'contracten'],
    text: 'Opstellen, versturen en nauwgezet opvolgen van digitale contracten voor uw cliënten.'
  },
  {
    id: 'facturatie',
    icon: faFileInvoiceDollar,
    title: ['Facturatie &', 'Subsidies'],
    text: 'Nauwkeurige facturatie (inclusief correctieronden) en verantwoording van subsidies zoals SMI en peuteropvang.'
  },
  {
    id: 'debiteurenadministratie',
    icon: faMoneyCheckDollar,
    title: ['Koppeling met', 'debiteurenadministratie'],
    text: 'Strakke opvolging van betalingen en een naadloze koppeling met Payt voor uw administratie.'
  },
  {
    id: 'advies',
    icon: faLightbulb,
    title: ['Ondersteuning bij', 'advies & beleid'],
    text: 'Deskundig advies en ondersteuning bij beleidsontwikkeling binnen de kinderopvangsector.'
  },
  {
    id: 'applicatiebeheer',
    icon: faLaptopCode,
    title: ['Applicatiebeheer', 'via Jaamo'],
    text: 'Volledig beheer van Jaamo, inclusief KOI-aanlevering en technische ondersteuning.'
  }
]

let animationContext: gsap.Context | null = null

const scrollToServices = () => {
  if (!transitionSection.value) return
  const transitionTrigger = ScrollTrigger.getById('hero-services-transition')
  const target = transitionTrigger
    ? transitionTrigger.start + (transitionTrigger.end - transitionTrigger.start) * 0.445
    : transitionSection.value.offsetTop + window.innerHeight * 1.4
  const smoother = ScrollSmoother.get()
  if (smoother) {
    smoother.scrollTo(target, true)
  } else {
    window.scrollTo({ top: target, behavior: 'smooth' })
  }
}

defineExpose({
  scrollToServices
})

onMounted(async () => {
  gsap.registerPlugin(ScrollTrigger, ScrollSmoother)
  await nextTick()

  animationContext = gsap.context(() => {

    const coverScale = () => {
      const diameter = Math.min(window.innerWidth, window.innerHeight) * 0.68
      return (Math.hypot(window.innerWidth, window.innerHeight) / diameter) * 1.08
    }

    const getScrollAmount = () => {
      if (!servicesTrack.value) return 0
      const padding = window.innerWidth < 768 ? 32 : 128
      return -(servicesTrack.value.scrollWidth - (window.innerWidth - padding))
    }

    const timeline = gsap.timeline({
      defaults: { ease: 'none' },
      scrollTrigger: {
        id: 'hero-services-transition',
        trigger: transitionSection.value,
        start: 'top top',
        end: '+=260%',
        scrub: 0.8,
        pin: true,
        invalidateOnRefresh: true
      }
    })

    timeline
      .to('.hero-layer', { opacity: 0, yPercent: -5, duration: 0.25 }, 0)
      .fromTo(
        '.sun-orb',
        { opacity: 0, scale: 0.16, left: '50%', top: '50%' },
        { opacity: 0.34, scale: 0.8, duration: 0.15 },
        0
      )
      .to('.sun-orb', { opacity: 1, scale: 1.32, duration: 0.15 }, 0.15)
      .to(
        '.sun-orb',
        {
          left: '50%',
          top: '50%',
          scale: coverScale,
          duration: 0.25
        },
        0.3
      )
      .set('.services-layer', { visibility: 'visible' }, 0.45)
      .fromTo(
        '.services-layer',
        { opacity: 0, y: 24 },
        { opacity: 1, y: 0, duration: 0.18 },
        0.48
      )

    if (servicesTrack.value) {
      timeline.to(
        servicesTrack.value,
        {
          x: getScrollAmount,
          duration: 0.8,
          ease: 'none'
        },
        0.65
      )
    }
  }, transitionSection.value ?? undefined)

  ScrollTrigger.refresh()
})

onBeforeUnmount(() => {
  animationContext?.revert()
})
</script>

<template>
  <section
    ref="transitionSection"
    class="relative w-full h-[100svh] min-h-[42rem] overflow-hidden isolation-isolate bg-lumi-navy text-lumi-white transform-gpu"
    aria-label="Introductie en diensten"
  >
    <!-- HERO LAYER -->
    <div class="hero-layer absolute inset-0 z-[2] grid place-items-center px-6 py-20 md:py-16 will-change-transform opacity-100">
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
          @click="scrollToServices"
        >
          Bekijk onze diensten
        </button>
      </div>
    </div>

    <!-- SUN ORB ANIMATION PIN CIRCLE -->
    <div
      class="sun-orb absolute z-[1] left-1/2 top-1/2 w-[68vmin] h-[68vmin] rounded-full bg-lumi-yellow opacity-0 -translate-x-1/2 -translate-y-1/2 scale-[0.16] origin-center will-change-transform"
      aria-hidden="true"
    />

    <!-- SERVICES LAYER WITH GSAP PINNED HORIZONTAL CARD SLIDE -->
    <div
      id="diensten"
      class="services-layer absolute inset-0 z-[3] invisible opacity-0 px-6 md:px-16 py-16 text-lumi-navy flex flex-col justify-center overflow-hidden will-change-transform"
    >
      <div class="w-full max-w-[100rem] mx-auto">
        <header class="mb-8">
          <h1>
            Onze diensten
          </h1>
          <p class="max-w-[42rem] mt-6 text-body-lg pl-2">
            Lorem ipsum dolor sit amet consectetur adipisicing elit. Eaque tempore voluptate explicabo? Repudiandae voluptatibus nemo eos, natus non cumque molestias explicabo consequuntur, vel amet eius officiis, iusto commodi accusantium aspernatur!
          </p>
        </header>

        <div
          ref="servicesTrack"
          class="services-track flex flex-nowrap gap-5 md:gap-6 will-change-transform"
        >
          <article
            v-for="service in services"
            :key="service.id"
            class="service-card flex flex-col p-6 md:p-7 rounded-2xl bg-white/97 text-lumi-navy shadow-lg gap-3 w-[290px] sm:w-[340px] md:w-[380px] flex-shrink-0"
          >
            <span class="inline-grid place-items-center w-14 h-14 rounded-full bg-lumi-gold-bg text-lumi-gold-text text-2xl" aria-hidden="true">
              <FontAwesomeIcon :icon="service.icon" />
            </span>
            <h3 class="text-lumi-navy">
              <span v-for="titleLine in service.title" :key="titleLine" class="block">{{ titleLine }}</span>
            </h3>
            <p class="text-body-md mt-1 leading-relaxed">
              {{ service.text }}
            </p>
          </article>
        </div>
      </div>
    </div>
  </section>
</template>
