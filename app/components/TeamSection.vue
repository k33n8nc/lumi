<script setup lang="ts">
import { ref } from 'vue'
import { ScrollSmoother } from 'gsap/ScrollSmoother'

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
    class="relative w-full min-h-screen flex flex-col justify-center py-20 md:py-28 px-6 md:px-16 bg-white text-lumi-navy overflow-hidden"
    aria-label="Ons team"
  >
    <div class="w-full max-w-[100rem] mx-auto grid grid-cols-1 lg:grid-cols-12 gap-12 lg:gap-16 items-center">
      <!-- Left Column: Copy -->
      <div class="lg:col-span-6 flex flex-col gap-6">
        <h1>
          Het team achter<br><em class="text-lumi-yellow not-italic">Lumi</em> Support
        </h1>
        <p class="text-body-lg text-slate-700 leading-relaxed max-w-lg">
          Onze persoonlijke aanpak maakt het verschil. Wij zijn een klein team met een grote focus
          op uw kwaliteit en rust.
        </p>
      </div>

      <!-- Right Column: Navy Orb (Static element) -->
      <div class="lg:col-span-6 flex items-center justify-center lg:justify-end">
        <div
          class="w-[50vmin] h-[50vmin] max-w-[480px] max-h-[480px] min-w-[240px] min-h-[240px] rounded-full bg-lumi-navy shadow-2xl"
          aria-hidden="true"
        />
      </div>
    </div>
  </section>
</template>
