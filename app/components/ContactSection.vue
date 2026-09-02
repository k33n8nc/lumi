<script setup lang="ts">
import { ref } from 'vue'
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'
import { faEnvelope, faPhone } from '@fortawesome/free-solid-svg-icons'
import { ScrollSmoother } from 'gsap/ScrollSmoother'

const sectionRef = ref<HTMLElement | null>(null)

const scrollToContact = () => {
  if (!sectionRef.value) return
  const smoother = ScrollSmoother.get()
  if (smoother) {
    smoother.scrollTo(sectionRef.value, true)
  } else {
    sectionRef.value.scrollIntoView({ behavior: 'smooth' })
  }
}

defineExpose({
  scrollToContact
})
</script>

<template>
  <section
    id="kennismaken"
    ref="sectionRef"
    class="relative w-full flex flex-col justify-center py-20 md:py-28 px-6 md:px-16 bg-lumi-yellow text-lumi-navy overflow-hidden"
    aria-label="Kennismaken en contact"
  >
    <div class="w-full max-w-[100rem] mx-auto grid grid-cols-1 lg:grid-cols-12 gap-12 lg:gap-16 items-center">
      <!-- Left Side: Contact Info -->
      <div class="lg:col-span-8 flex flex-col gap-8">
        <div>
          <h1 class="text-lumi-navy">
            Laten we kennismaken
          </h1>
          <p class="mt-4 text-body-lg text-slate-800 leading-relaxed max-w-xl">
            Wilt u weten wat Lumi Support voor uw kinderopvangorganisatie kan betekenen?
            Neem vandaag nog contact met ons op.
          </p>
        </div>

        <div class="flex flex-col gap-5 pt-4 border-lumi-navy/15 max-w-xl">
          <!-- Mail Option -->
          <a
            href="mailto:contact@lumi-support.nl"
            class="flex items-center gap-4 text-lumi-navy"
          >
            <span class="inline-grid place-items-center w-12 h-12 rounded-full bg-lumi-navy/10 text-lumi-navy text-xl" aria-hidden="true">
              <FontAwesomeIcon :icon="faEnvelope" />
            </span>
            <div class="flex flex-col">
              <span class="text-xs uppercase tracking-wider text-lumi-navy/60 font-bold">Mail ons</span>
              <span class="text-base sm:text-lg font-bold">contact@lumi-support.nl</span>
            </div>
          </a>

          <!-- Phone Option -->
          <a
            href="tel:+31640937499"
            class="flex items-center gap-4 text-lumi-navy hover:text-black transition-colors group no-underline"
          >
            <span class="inline-grid place-items-center w-12 h-12 rounded-full bg-lumi-navy/10 text-lumi-navy text-xl" aria-hidden="true">
              <FontAwesomeIcon :icon="faPhone" />
            </span>
            <div class="flex flex-col">
              <span class="text-xs uppercase tracking-wider text-lumi-navy/60 font-bold">Bel ons</span>
              <span class="text-base sm:text-lg font-bold">+31 (0)6 40937499</span>
            </div>
          </a>
        </div>
      </div>
    </div>
  </section>
</template>
