<script setup lang="ts">
import { ref } from 'vue'
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
import { ScrollSmoother } from 'gsap/ScrollSmoother'

const sectionRef = ref<HTMLElement | null>(null)

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
    title: ['Koppeling met', 'debiteurenbeheer'],
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

const scrollToServices = () => {
  if (!sectionRef.value) return
  const smoother = ScrollSmoother.get()
  if (smoother) {
    smoother.scrollTo(sectionRef.value, true)
  } else {
    sectionRef.value.scrollIntoView({ behavior: 'smooth' })
  }
}

defineExpose({
  scrollToServices
})
</script>

<template>
  <section
    id="diensten"
    ref="sectionRef"
    class="relative w-full min-h-screen flex flex-col justify-center py-20 md:py-28 px-6 md:px-16 bg-lumi-navy text-white/90 overflow-hidden"
    aria-label="Onze diensten"
  >
    <div class="w-full max-w-[100rem] mx-auto flex flex-col">
      <!-- Centered Section Header -->
      <header class="mb-10 md:mb-14 text-center">
        <h1 class="text-white">
          Dit nemen wij uit handen
        </h1>
      </header>

      <!-- 2-Column Split: Left 8 cards (2 cols), Right text -->
      <div class="grid grid-cols-1 lg:grid-cols-12 gap-8 lg:gap-12 xl:gap-16 items-center">
        <!-- Left: 8 service cards in 2 columns (4 rows) -->
        <div class="lg:col-span-7 grid grid-cols-1 sm:grid-cols-2 auto-rows-fr gap-4 sm:gap-5">
          <article
            v-for="service in services"
            :key="service.id"
            class="service-card flex flex-col h-full p-5 sm:p-6 rounded-2xl bg-white/8 hover:bg-white/14 hover:border-lumi-yellow/40 border border-white/5 backdrop-blur-md shadow-md transition-all duration-300 gap-3"
          >
            <span class="inline-grid place-items-center w-12 h-12 rounded-full bg-white/10 text-lumi-yellow text-xl flex-shrink-0" aria-hidden="true">
              <FontAwesomeIcon :icon="service.icon" />
            </span>
            <h3 class="text-white font-bold text-lg leading-snug">
              <span v-for="titleLine in service.title" :key="titleLine" class="block">{{ titleLine }}</span>
            </h3>
          </article>
        </div>

        <!-- Right: "Tijdelijk extra expertise nodig?" with Lamp Light Effect -->
        <div class="relative z-10 lg:col-span-5 flex flex-col items-center text-center justify-center pt-4 lg:pt-0">
          
          <!-- LOGO WITH SUBTLE LIGHT EFFECT -->
          <div class="relative flex flex-col items-center">
            <!-- SUBTLE ROUNDED LIGHT BEAM (LUMI YELLOW) -->
            <div class="pointer-events-none absolute -top-4 sm:-top-6 left-1/2 -translate-x-1/2 w-[520px] sm:w-[620px] lg:w-[680px] h-[500px] sm:h-[560px] -z-10 select-none overflow-visible" aria-hidden="true">
              <svg
                class="w-full h-full overflow-visible"
                viewBox="0 0 800 600"
                fill="none"
                xmlns="http://www.w3.org/2000/svg"
              >
                <defs>
                  <!-- Subtle Lumi Yellow Gradient -->
                  <linearGradient id="lumiServicesBeam" x1="400" y1="20" x2="400" y2="600" gradientUnits="userSpaceOnUse">
                    <stop offset="0%" stop-color="#ffd24a" stop-opacity="0.22" />
                    <stop offset="30%" stop-color="#ffd24a" stop-opacity="0.12" />
                    <stop offset="65%" stop-color="#ffd24a" stop-opacity="0.04" />
                    <stop offset="100%" stop-color="#ffd24a" stop-opacity="0" />
                  </linearGradient>

                  <!-- Soft Gaussian Blur Filter -->
                  <filter id="servicesSubtleGlow" x="-20%" y="-20%" width="140%" height="140%">
                    <feGaussianBlur stdDeviation="16" />
                  </filter>
                </defs>

                <!-- Rounded dome top expanding into smooth light cone -->
                <path
                  d="M 355 70 C 355 20, 445 20, 445 70 L 740 590 C 740 590, 400 600, 60 590 Z"
                  fill="url(#lumiServicesBeam)"
                  filter="url(#servicesSubtleGlow)"
                />
              </svg>

              <!-- Soft ambient glow right behind the bulb -->
              <div class="absolute top-2 left-1/2 -translate-x-1/2 -translate-y-1/4 w-[160px] h-[160px] rounded-full bg-[radial-gradient(circle,rgba(255,210,74,0.25)_0%,rgba(255,210,74,0.08)_45%,transparent_70%)] blur-[18px]" />
            </div>

            <!-- LOGO IMAGE -->
            <div class="relative mb-5 md:mb-6">
              <img
                src="~/assets/images/logo-trans-kleur-wit.png"
                alt="Lumi Logo"
                class="relative z-10 w-16 h-auto sm:w-18 md:w-20 select-none drop-shadow-[0_0_16px_rgba(255,210,74,0.45)]"
              />
            </div>
          </div>

          <!-- Text content illuminated by the light beam -->
          <div class="relative z-10 max-w-lg flex flex-col gap-4">
            <h2 class="text-white text-2xl sm:text-3xl font-bold tracking-tight">
              Tijdelijk extra expertise nodig?
            </h2>
            <div class="flex flex-col gap-4 text-slate-200 text-body-lg leading-relaxed">
              <p>
                Bij ziekte, zwangerschapsverlof, personeelstekort of tijdelijke extra drukte kunnen jullie direct op ons rekenen. Lumi Support levert ervaren interim planners en financieel-administratieve medewerkers die snel inzetbaar zijn en de kinderopvang kennen.
              </p>
              <p>
                We nemen de werkzaamheden tijdelijk uit handen en zorgen dat de administratie deskundig, zorgvuldig en zonder onderbreking doorgaat. Zo blijft de continuïteit gewaarborgd, juist op de momenten dat jullie extra ondersteuning nodig hebben.
              </p>
            </div>
          </div>

        </div>
      </div>
    </div>
  </section>
</template>
