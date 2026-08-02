<script setup lang="ts">
import { nextTick, onBeforeUnmount, onMounted, ref } from 'vue'
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'
import { faEnvelope, faPhone } from '@fortawesome/free-solid-svg-icons'
import gsap from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'
import logoImg from '~/assets/images/logo.png'

const sectionRef = ref<HTMLElement | null>(null)

let animationContext: gsap.Context | null = null

const scrollToTeam = () => {
  if (!sectionRef.value) return
  const trigger = ScrollTrigger.getById('team-contact-transition')
  const target = trigger ? trigger.start + 2 : sectionRef.value.offsetTop
  window.scrollTo({ top: target, behavior: 'smooth' })
}

const scrollToContact = () => {
  if (!sectionRef.value) return
  const trigger = ScrollTrigger.getById('team-contact-transition')
  const target = trigger
    ? trigger.start + (trigger.end - trigger.start) * 0.75
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
    gsap.set('.team-copy', { xPercent: -120 })
    gsap.set('.navy-orb', { opacity: 0 })
    gsap.set('.contact-layer', { opacity: 1, visibility: 'visible' })
    return
  }

  animationContext = gsap.context(() => {
    const coverScale = () => {
      const diameter = Math.min(window.innerWidth, window.innerHeight) * 0.64
      return (Math.hypot(window.innerWidth, window.innerHeight) / (diameter || 1)) * 2.5
    }

    const timeline = gsap.timeline({
      defaults: { ease: 'none' },
      scrollTrigger: {
        id: 'team-contact-transition',
        trigger: sectionRef.value,
        start: 'top top',
        end: '+=180%',
        scrub: 0.8,
        pin: true,
        invalidateOnRefresh: true
      }
    })

    timeline
      // 1. Team copy slides left off-screen immediately on scroll start
      .to('.team-copy', { xPercent: -120, duration: 0.2 }, 0)
      // 2. Navy orb starts expanding immediately at scroll start
      .to(
        '.navy-orb',
        {
          left: '50%',
          top: '50%',
          right: 'auto',
          xPercent: -50,
          yPercent: -50,
          scale: coverScale,
          duration: 0.5
        },
        0
      )
      // 3. Reveal parent contact layer container right at scroll start (0.0)
      .set('.contact-layer', { visibility: 'visible' }, 0)
      .to('.contact-layer', { opacity: 1, duration: 0.05 }, 0)
      // 4. Logo reveals immediately right as circle starts growing (0.01)
      .fromTo(
        '.lumi-logo-img',
        { opacity: 0, scale: 0.85 },
        { opacity: 1, scale: 1, duration: 0.28 },
        0.01
      )
      // 5. Contact info reveals immediately after (0.05)
      .fromTo(
        '.contact-info',
        { opacity: 0, x: 40 },
        { opacity: 1, x: 0, duration: 0.32 },
        0.05
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
    class="relative w-full h-[100svh] min-h-[42rem] overflow-hidden isolation-isolate bg-white text-lumi-navy flex items-center justify-center transform-gpu"
    aria-label="Team en kennismaken"
  >
    <!-- LAYER 1: TEAM COPY (Starts Visible, slides left faster immediately on scroll) -->
    <div
      id="ons-team"
      class="team-layer absolute inset-0 z-[2] flex items-center px-6 md:px-16 py-16 text-lumi-navy will-change-transform"
    >
      <div class="w-full max-w-[100rem] mx-auto grid grid-cols-1 lg:grid-cols-12 gap-10 lg:gap-16 items-center">
        <div class="team-copy lg:col-span-6 flex flex-col gap-6 will-change-transform">
          <h2>
            Het team achter<br><em class="text-lumi-yellow not-italic">Lumi</em> Support
          </h2>
          <p class="text-body-lg text-slate-700 leading-relaxed max-w-lg">
            Onze persoonlijke aanpak maakt het verschil. Wij zijn een klein team met een grote focus
            op uw kwaliteit en rust.
          </p>
        </div>
      </div>
    </div>

    <!-- LAYER 2: EXPANDING NAVY ORB CIRCLE -->
    <div
      class="navy-orb absolute z-[1] right-20 md:right-[8.5rem] top-1/2 -translate-y-1/2 w-[64vmin] h-[64vmin] max-w-[620px] max-h-[620px] rounded-full bg-lumi-navy opacity-100 origin-center will-change-transform transform-gpu"
      aria-hidden="true"
    />

    <!-- LAYER 3: CONTACT & LOGO LAYER (z-[10] above expanding orb) -->
    <div
      id="kennismaken"
      class="contact-layer absolute inset-0 z-[10] invisible opacity-0 flex items-center px-6 md:px-16 py-16 text-white will-change-transform pointer-events-auto"
    >
      <div class="w-full max-w-[100rem] mx-auto grid grid-cols-1 lg:grid-cols-12 gap-12 lg:gap-16 items-center">
        <!-- Left Side: Contact Info -->
        <div class="contact-info lg:col-span-7 flex flex-col gap-8 will-change-transform">
          <div>
            <h2 class="text-lumi-yellow">
              Laten we kennismaken
            </h2>
            <p class="mt-4 text-body-lg text-slate-300 leading-relaxed max-w-xl">
              Wilt u weten wat Lumi Support voor uw kinderopvangorganisatie kan betekenen?
              Neem vandaag nog contact met ons op.
            </p>
          </div>

          <div class="flex flex-col gap-5 pt-4 border-t border-white/15 max-w-xl">
            <!-- Mail Option -->
            <a
              href="mailto:contact@lumi-support.nl"
              class="flex items-center gap-4 text-white hover:text-lumi-yellow transition-colors group no-underline"
            >
              <span class="inline-grid place-items-center w-12 h-12 rounded-full bg-white text-lumi-navy text-lg group-hover:scale-105 transition-transform" aria-hidden="true">
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
              <span class="inline-grid place-items-center w-12 h-12 rounded-full bg-white text-lumi-navy text-lg group-hover:scale-105 transition-transform" aria-hidden="true">
                <FontAwesomeIcon :icon="faPhone" />
              </span>
              <div class="flex flex-col">
                <span class="text-xs uppercase tracking-wider text-slate-400 font-bold">Bel ons</span>
                <span class="text-base sm:text-lg font-medium">+31 (0)6 40937499</span>
              </div>
            </a>
          </div>
        </div>

        <!-- Right Side: Inflated White LUMI Bulb Logo -->
        <div class="logo-wrapper lg:col-span-5 flex flex-col items-center justify-center text-center">
          <img
            :src="logoImg"
            alt="Lumi Support Logo"
            class="lumi-logo-img w-56 sm:w-72 md:w-84 lg:w-[26rem] h-auto mb-4 drop-shadow-xl will-change-transform"
          />
        </div>
      </div>
    </div>
  </section>
</template>
