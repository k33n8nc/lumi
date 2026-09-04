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
    class="relative w-full flex flex-col justify-center py-20 md:py-28 px-6 md:px-16 bg-lumi-navy text-white/90"
    aria-label="Onze diensten"
  >
    <div class="w-full">
      <header class="mb-10 md:mb-12">
        <h1 class="">
          Dit nemen wij uit handen
        </h1>
      </header>

      <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 auto-rows-fr gap-5 md:gap-6">
        <article
          v-for="service in services"
          :key="service.id"
          class="service-card flex flex-col h-full p-6 md:p-7 rounded-2xl bg-white/8 hover:bg-white/14 hover:border-lumi-yellow/40 backdrop-blur-md shadow-md transition-all duration-300 gap-3"
        >
          <span class="inline-grid place-items-center w-12 h-12 rounded-full bg-white/10 text-lumi-yellow text-xl" aria-hidden="true">
            <FontAwesomeIcon :icon="service.icon" />
          </span>
          <h3 class="text-white">
            <span v-for="titleLine in service.title" :key="titleLine" class="block">{{ titleLine }}</span>
          </h3>
          <!-- <p class="text-slate-300 text-body-md leading-relaxed">
            {{ service.text }}
          </p> -->
        </article>
      </div>
      <div class="max-w-2xl">
          <h3 id="beliefs-title" class="text-white mt-8 mb-2">
            Tijdelijk extra expertise nodig?
          </h3>
          <p>
            Tijdelijk extra expertise nodig? Bij ziekte, zwangerschapsverlof, personeelstekort of tijdelijke extra drukte kunnen jullie direct op ons rekenen. Lumi Support levert ervaren interim planners en financieel-administratieve medewerkers die snel inzetbaar zijn en de kinderopvang kennen.
          </p>
          <p class="mt-4">
            We nemen de werkzaamheden tijdelijk uit handen en zorgen dat de administratie deskundig, zorgvuldig en zonder onderbreking doorgaat. Zo blijft de continuïteit gewaarborgd, juist op de momenten dat jullie extra ondersteuning nodig hebben.
          </p>
      </div>
    </div>
  </section>
</template>
