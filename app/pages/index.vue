<script setup lang="ts">
import { ref } from 'vue'
import gsap from 'gsap'

useHead({
  title: 'Lumi | Helderheid in uw organisatie',
  meta: [
    {
      name: 'description',
      content: 'Lumi Support brengt rust, overzicht en continuïteit in kinderopvangorganisaties.'
    }
  ]
})

const beliefsRef = ref<{ scrollToBeliefs: () => void } | null>(null)
const servicesRef = ref<{ scrollToServices: () => void } | null>(null)
const teamRef = ref<{ scrollToTeam: () => void } | null>(null)
const contactRef = ref<{ scrollToContact: () => void } | null>(null)

const onNavigate = (sectionId: string) => {
  if (sectionId === 'hero') {
    window.scrollTo({ top: 0, behavior: 'smooth' })
  } else if (sectionId === 'visie' || sectionId === 'geloven-wij-in') {
    beliefsRef.value?.scrollToBeliefs()
  } else if (sectionId === 'diensten') {
    servicesRef.value?.scrollToServices()
  } else if (sectionId === 'team') {
    teamRef.value?.scrollToTeam()
  } else if (sectionId === 'contact') {
    contactRef.value?.scrollToContact()
  } else {
    const el = document.getElementById(sectionId)
    if (el) {
      el.scrollIntoView({ behavior: 'smooth' })
    }
  }
}
</script>

<template>
  <div>
    <!-- Fixed Viewport Navigation -->
    <AppNavigation @navigate="onNavigate" />

    <main class="min-h-screen">
      <!-- Standalone Static Hero Section -->
      <HeroSection
        @scroll-to-beliefs="() => onNavigate('visie')"
        @scroll-to-services="() => onNavigate('diensten')"
      />

      <!-- Beliefs / Visie Section -->
      <BeliefsSection
        ref="beliefsRef"
        @scroll-to-services="() => onNavigate('diensten')"
      />

      <!-- Standalone Services Section -->
      <ServicesSection ref="servicesRef" />

      <!-- Standalone Team Section -->
      <TeamSection ref="teamRef" />

      <!-- Standalone Contact Section -->
      <ContactSection ref="contactRef" />

      <!-- Footer Section -->
      <AppFooter @navigate="onNavigate" />
    </main>
  </div>
</template>
