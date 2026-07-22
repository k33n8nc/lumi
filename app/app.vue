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

const transitionSection = ref<HTMLElement | null>(null)
const horizontalSection = ref<HTMLElement | null>(null)
const menuOpen = ref(false)

const services = [
  { number: '01', title: 'Planning', text: 'Grip op bezetting, roosters en de dagelijkse praktijk.' },
  { number: '02', title: 'Oudercommunicatie', text: 'Heldere, zorgvuldige communicatie die vertrouwen geeft.' },
  { number: '03', title: 'Facturatie', text: 'Een correct en overzichtelijk facturatieproces.' },
  { number: '04', title: 'Debiteurenbeheer', text: 'Persoonlijke opvolging met aandacht voor de relatie.' },
  { number: '05', title: 'Administratie', text: 'Een administratie die klopt en altijd inzicht biedt.' },
  { number: '06', title: 'Continuïteit', text: 'Extra capaciteit en kennis precies wanneer die nodig is.' }
]

let smoother: ScrollSmoother | null = null
let animationContext: gsap.Context | null = null
let horizontalContext: gsap.Context | null = null

const scrollToServices = () => {
  if (!transitionSection.value) return

  const target = transitionSection.value.offsetTop + window.innerHeight * 2.92
  window.scrollTo({ top: target, behavior: 'smooth' })
}

const scrollToTop = () => {
  menuOpen.value = false
  window.scrollTo({ top: 0, behavior: 'smooth' })
}

const scrollToTeam = () => {
  menuOpen.value = false
  const horizontalTrigger = ScrollTrigger.getById('team-contact-transition')
  const target = horizontalTrigger?.start ?? horizontalSection.value?.getBoundingClientRect().top ?? 0
  window.scrollTo({ top: target, behavior: 'smooth' })
}

const scrollToContact = () => {
  menuOpen.value = false
  const horizontalTrigger = ScrollTrigger.getById('team-contact-transition')
  const target = horizontalTrigger?.end ?? horizontalSection.value?.getBoundingClientRect().top ?? 0
  window.scrollTo({ top: target, behavior: 'smooth' })
}

onMounted(async () => {
  gsap.registerPlugin(ScrollTrigger, ScrollSmoother)
  await nextTick()

  const prefersReducedMotion = window.matchMedia('(prefers-reduced-motion: reduce)').matches

  if (!prefersReducedMotion) {
    smoother = ScrollSmoother.create({
      wrapper: '#smooth-wrapper',
      content: '#smooth-content',
      smooth: 1.15,
      effects: true,
      normalizeScroll: true,
      smoothTouch: 0.08
    })
  }

  animationContext = gsap.context(() => {
    if (prefersReducedMotion) {
      gsap.set('.sun-orb', { opacity: 1, scale: 4, left: '50%', top: '50%' })
      gsap.set('.hero-layer', { opacity: 0 })
      gsap.set('.services-layer', { opacity: 1, visibility: 'visible' })
      return
    }

    const coverScale = () => {
      const diameter = Math.min(window.innerWidth, window.innerHeight) * 0.68
      return (Math.hypot(window.innerWidth, window.innerHeight) / diameter) * 1.08
    }

    const timeline = gsap.timeline({
      defaults: { ease: 'none' },
      scrollTrigger: {
        trigger: transitionSection.value,
        start: 'top top',
        end: '+=300%',
        scrub: 0.8,
        pin: true,
        anticipatePin: 1,
        invalidateOnRefresh: true
      }
    })

    timeline
      .to('.hero-layer', { opacity: 0.22, yPercent: -2, duration: 0.2 }, 0.06)
      .to('.hero-cta', { opacity: 0, y: -12, duration: 0.12 }, 0.04)
      .fromTo(
        '.sun-orb',
        { opacity: 0, scale: 0.16, left: '50%', top: '50%' },
        { opacity: 0.34, scale: 0.8, duration: 0.24 },
        0.06
      )
      .to('.hero-layer', { opacity: 0, yPercent: -5, duration: 0.18 }, 0.26)
      .to('.sun-orb', { opacity: 1, scale: 1.32, duration: 0.26 }, 0.24)
      .to('.sun-orb', {
        left: '50%',
        top: '50%',
        scale: coverScale,
        duration: 0.42
      }, 0.5)
      .set('.services-layer', { visibility: 'visible' }, 0.58)
      .fromTo(
        '.services-layer',
        { opacity: 0, y: 32 },
        { opacity: 1, y: 0, duration: 0.27 },
        0.66
      )
      .fromTo(
        '.service-card',
        { opacity: 0, y: 24 },
        { opacity: 1, y: 0, duration: 0.22, stagger: 0.025 },
        0.7
      )
  }, transitionSection.value ?? undefined)

  if (!prefersReducedMotion) {
    horizontalContext = gsap.context(() => {
      gsap.to('.horizontal-track', {
        xPercent: -50,
        ease: 'none',
        scrollTrigger: {
          id: 'team-contact-transition',
          trigger: horizontalSection.value,
          start: 'top top',
          end: '+=100%',
          scrub: 0.8,
          pin: true,
          anticipatePin: 1,
          invalidateOnRefresh: true
        }
      })
    }, horizontalSection.value ?? undefined)
  }

  ScrollTrigger.refresh()
})

onBeforeUnmount(() => {
  animationContext?.revert()
  horizontalContext?.revert()
  smoother?.kill()
  ScrollTrigger.getAll().forEach(trigger => trigger.kill())
})
</script>

<template>
  <div id="smooth-wrapper">
    <div id="smooth-content">
      <main>
        <section ref="transitionSection" class="transition-stage" aria-label="Introductie en diensten">
          <button
            class="menu-button"
            type="button"
            :aria-expanded="menuOpen"
            aria-label="Menu openen"
            @click="menuOpen = !menuOpen"
          >
            <span />
            <span />
            <span />
          </button>

          <div class="hero-layer">
            <div class="hero-copy">
              <h1>Lumi brengt <em>helderheid</em><br>in uw organisatie.</h1>
              <p>
                Lumi Support staat naast kinderopvangorganisaties die rust, overzicht en continuïteit zoeken.
                Met jarenlange praktijkervaring binnen de kinderopvang weten wij precies waar de uitdagingen
                liggen - van planning en oudercommunicatie tot facturatie en debiteurenbeheer.
              </p>
              <button class="hero-cta" type="button" @click="scrollToServices">
                Bekijk onze diensten
              </button>
            </div>
          </div>

          <div class="sun-orb" aria-hidden="true" />

          <div id="diensten" class="services-layer">
            <div class="services-inner">
              <header class="services-heading">
                <h2>Onze diensten</h2>
              </header>

              <div class="services-grid">
                <article v-for="service in services" :key="service.number" class="service-card">
                  <span>{{ service.number }}</span>
                  <div>
                    <h3>{{ service.title }}</h3>
                    <p>{{ service.text }}</p>
                  </div>
                </article>
              </div>
            </div>
          </div>

          <Transition name="menu-fade">
            <nav v-if="menuOpen" class="menu-panel" aria-label="Hoofdnavigatie">
              <button type="button" @click="scrollToTop">Home</button>
              <button type="button" @click="menuOpen = false; scrollToServices()">Onze diensten</button>
              <button type="button" @click="scrollToTeam">Ons team</button>
              <button type="button" @click="scrollToContact">Kennismaken</button>
            </nav>
          </Transition>
        </section>

        <section ref="horizontalSection" class="horizontal-stage" aria-label="Team en kennismaken">
          <div class="horizontal-track">
            <section id="ons-team" class="team-panel" aria-labelledby="team-title">
              <div class="team-copy">
                <h2 id="team-title">Het team achter<br><em>Lumi</em> Support</h2>
                <p>
                  Onze persoonlijke aanpak maakt het verschil. Wij zijn een klein team met een grote focus
                  op uw kwaliteit en rust.
                </p>
              </div>

              <div class="team-visual" aria-label="Ruimte voor toekomstige teamfoto">
                <span>Team Lumi</span>
              </div>
            </section>

            <section id="kennismaken" class="contact-panel" aria-labelledby="contact-title">
              <div class="contact-shell">
                <div class="contact-intro">
                  <div>
                    <h2 id="contact-title">Laten we kennismaken</h2>
                    <p>
                      Wilt u weten wat Lumi Support voor uw kinderopvangorganisatie kan betekenen?
                      Neem vandaag nog contact met ons op.
                    </p>
                  </div>

                  <div class="contact-options">
                    <a href="mailto:contact@lumi-support.nl" class="contact-option">
                      <span class="contact-icon" aria-hidden="true" />
                      <span><small>Mail ons</small>contact@lumi-support.nl</span>
                    </a>
                    <a href="tel:+31640937499" class="contact-option">
                      <span class="contact-icon" aria-hidden="true" />
                      <span><small>Bel ons</small>+31 (0)6 40937499</span>
                    </a>
                  </div>
                </div>

                <form class="contact-form" @submit.prevent>
                  <label>
                    <span>Naam</span>
                    <input type="text" name="name" autocomplete="name">
                  </label>
                  <label>
                    <span>E-mailadres</span>
                    <input type="email" name="email" autocomplete="email">
                  </label>
                  <label class="message-field">
                    <span>Bericht</span>
                    <textarea name="message" />
                  </label>
                  <button type="submit">Verstuur bericht</button>
                </form>
              </div>
            </section>
          </div>
        </section>

        <section class="closing-section">
          <p>Administratieve rust voor de kinderopvang.</p>
          <a href="mailto:info@lumi-support.nl">Plan een kennismaking <span>↗</span></a>
        </section>
      </main>
    </div>
  </div>
</template>
