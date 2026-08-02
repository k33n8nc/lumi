<script setup lang="ts">
import { ref } from 'vue'

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

const onNavigate = (sectionId: string) => {
  if (sectionId === 'hero') {
    window.scrollTo({ top: 0, behavior: 'smooth' })
  } else if (sectionId === 'diensten') {
    heroServicesRef.value?.scrollToServices()
  } else if (sectionId === 'team') {
    teamContactRef.value?.scrollToTeam()
  } else if (sectionId === 'contact') {
    teamContactRef.value?.scrollToContact()
  } else if (sectionId === 'werken-bij' || sectionId === 'careers') {
    careersRef.value?.scrollToCareers()
  } else {
    const el = document.getElementById(sectionId)
    if (el) {
      el.scrollIntoView({ behavior: 'smooth' })
    }
  }
}
</script>

<template>
  <main class="min-h-screen bg-lumi-navy">
    <!-- Header Navigation -->
    <AppNavigation @navigate="onNavigate" />

    <!-- Hero & Services Pinned GSAP Transition Section -->
    <HeroServicesSection ref="heroServicesRef" />

    <!-- Team & Contact Navy Orb Transition Section -->
    <TeamContactSection ref="teamContactRef" />

    <!-- Careers Section -->
    <CareersSection ref="careersRef" />

    <!-- Footer Section -->
    <AppFooter @navigate="onNavigate" />
  </main>
</template>
