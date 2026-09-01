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

const servicesSection = ref<HTMLElement | null>(null)
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
  if (!servicesSection.value) return
  const trigger = ScrollTrigger.getById('services-horizontal-track')
  const target = trigger ? trigger.start : servicesSection.value.offsetTop
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
    const getScrollAmount = () => {
      if (!servicesTrack.value) return 0
      const padding = window.innerWidth < 768 ? 32 : 128
      return -(servicesTrack.value.scrollWidth - (window.innerWidth - padding))
    }

    const timeline = gsap.timeline({
      defaults: { ease: 'none' },
      scrollTrigger: {
        id: 'services-horizontal-track',
        trigger: servicesSection.value,
        start: 'top top',
        end: '+=180%',
        scrub: 0.8,
        pin: true,
        anticipatePin: 1,
        invalidateOnRefresh: true
      }
    })

    if (servicesTrack.value) {
      timeline.to(
        servicesTrack.value,
        {
          x: getScrollAmount,
          duration: 1,
          ease: 'none'
        },
        0
      )
    }
  }, servicesSection.value ?? undefined)

  ScrollTrigger.refresh()
})

onBeforeUnmount(() => {
  animationContext?.revert()
})
</script>

<template>
  <div class="w-full bg-lumi-yellow overflow-hidden">
    <section
      id="diensten"
      ref="servicesSection"
      class="relative w-full h-screen min-h-[42rem] overflow-hidden bg-lumi-yellow text-lumi-navy flex flex-col justify-center px-6 md:px-16 py-16 will-change-transform transform-gpu"
      aria-label="Onze diensten"
    >
      <div class="w-full max-w-[100rem] mx-auto">
        <header class="mb-8">
          <h1>
            Onze diensten
          </h1>
          <p class="max-w-[42rem] mt-6 text-body-lg pl-2">
            Lumi Support ontzorgt kinderopvangorganisaties met gespecialiseerde administratieve, operationele en strategische ondersteuning.
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
    </section>
  </div>
</template>
