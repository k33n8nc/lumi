<script setup lang="ts">
import { nextTick, onBeforeUnmount, onMounted, ref } from 'vue'
import gsap from 'gsap'
import { ScrollSmoother } from 'gsap/ScrollSmoother'
import { ScrollTrigger } from 'gsap/ScrollTrigger'

useHead({
  title: 'Lumi | Helderheid in uw organisatie',
  meta: [
    {
      name: 'description',
      content: 'Lumi Support brengt rust, overzicht en continuïteit in kinderopvangorganisaties.'
    }
  ]
})

const heroServicesRef = ref<{ scrollToServices: () => void } | null>(null)
const teamContactRef = ref<{ scrollToTeam: () => void, scrollToContact: () => void } | null>(null)
const careersRef = ref<{ scrollToCareers: () => void } | null>(null)

let smoother: ScrollSmoother | null = null

const onNavigate = (sectionId: string) => {
  if (sectionId === 'hero') {
    if (smoother) {
      smoother.scrollTo(0, true)
    } else {
      window.scrollTo({ top: 0, behavior: 'smooth' })
    }
  } else if (sectionId === 'diensten') {
    heroServicesRef.value?.scrollToServices()
  } else if (sectionId === 'team') {
    teamContactRef.value?.scrollToTeam()
  } else if (sectionId === 'contact') {
    teamContactRef.value?.scrollToContact()
  } else if (sectionId === 'werken-bij') {
    careersRef.value?.scrollToCareers()
  } else {
    const el = document.getElementById(sectionId)
    if (el) {
      if (smoother) {
        smoother.scrollTo(el, true)
      } else {
        el.scrollIntoView({ behavior: 'smooth' })
      }
    }
  }
}

onMounted(async () => {
  gsap.registerPlugin(ScrollTrigger, ScrollSmoother)
  await nextTick()

  // Prevent mobile Safari address bar show/hide from thrashing ScrollTrigger refreshes
  ScrollTrigger.config({ ignoreMobileResize: true })

  // Enable ScrollSmoother on desktop. On mobile touch devices, native momentum scrolling
  // allows GSAP ScrollTrigger pins to run with 100% native GPU position: fixed hardware acceleration.
  if (ScrollTrigger.isTouch !== 1) {
    smoother = ScrollSmoother.create({
      wrapper: '#smooth-wrapper',
      content: '#smooth-content',
      smooth: 1.15,
      effects: true
    })
  }
})

onBeforeUnmount(() => {
  smoother?.kill()
})
</script>

<template>
  <div>
    <!-- Fixed Viewport Navigation (Outside smooth-content to prevent CSS transform trapping) -->
    <AppNavigation @navigate="onNavigate" />

    <!-- GSAP Smooth Scroll Wrapper -->
    <div id="smooth-wrapper">
      <div id="smooth-content">
        <main class="min-h-screen bg-lumi-navy">
          <!-- Hero & Services Pinned GSAP Transition Section -->
          <HeroServicesSection ref="heroServicesRef" />

          <!-- Team & Contact Navy Orb Transition Section -->
          <TeamContactSection ref="teamContactRef" />

          <!-- Careers Section -->
          <CareersSection ref="careersRef" />

          <!-- Footer Section -->
          <AppFooter @navigate="onNavigate" />
        </main>
      </div>
    </div>
  </div>
</template>
