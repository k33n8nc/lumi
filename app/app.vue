<script setup>
import { onMounted, ref } from 'vue'
import gsap from 'gsap'

// Refs for GSAP animation
const heroBadge = ref(null)
const heroTitle = ref(null)
const heroSub = ref(null)
const heroCtas = ref(null)
const heroVisual = ref(null)

onMounted(() => {
  // Stagger animate elements on mount
  const tl = gsap.timeline({ defaults: { ease: 'power4.out' } })
  
  tl.fromTo(heroBadge.value, 
    { opacity: 0, y: 20 }, 
    { opacity: 1, y: 0, duration: 0.6 }
  )
  .fromTo(heroTitle.value, 
    { opacity: 0, y: 30 }, 
    { opacity: 1, y: 0, duration: 0.8 }, 
    '-=0.4'
  )
  .fromTo(heroSub.value, 
    { opacity: 0, y: 20 }, 
    { opacity: 1, y: 0, duration: 0.6 }, 
    '-=0.5'
  )
  .fromTo(heroCtas.value, 
    { opacity: 0, y: 15 }, 
    { opacity: 1, y: 0, duration: 0.5 }, 
    '-=0.4'
  )
  .fromTo(heroVisual.value, 
    { opacity: 0, scale: 0.96, y: 40 }, 
    { opacity: 1, scale: 1, y: 0, duration: 1.0, ease: 'back.out(1.1)' }, 
    '-=0.5'
  )

  // Floating effects for elements in the mock UI
  gsap.to('.float-element-1', {
    y: -10,
    duration: 4,
    repeat: -1,
    yoyo: true,
    ease: 'power1.inOut'
  })
  gsap.to('.float-element-2', {
    y: 10,
    duration: 4.5,
    repeat: -1,
    yoyo: true,
    ease: 'power1.inOut',
    delay: 0.5
  })
})
</script>

<template>
  <div class="min-h-screen bg-zinc-950 text-zinc-50 font-sans selection:bg-brand-500 selection:text-zinc-950 relative overflow-hidden">
    <!-- Background Gradients -->
    <div class="absolute top-0 left-1/2 -translate-x-1/2 w-full max-w-7xl h-[600px] pointer-events-none overflow-hidden z-0">
      <div class="absolute top-[-10%] left-[20%] w-[500px] h-[500px] rounded-full bg-emerald-500/10 blur-[120px]"></div>
      <div class="absolute top-[-5%] right-[25%] w-[400px] h-[400px] rounded-full bg-green-400/5 blur-[100px]"></div>
    </div>

    <!-- Navigation Header -->
    <header class="border-b border-zinc-900 bg-zinc-950/80 backdrop-blur-md sticky top-0 z-50 transition-colors duration-300">
      <nav class="max-w-7xl mx-auto px-6 h-20 flex items-center justify-between">
        <!-- Logo -->
        <a href="#" class="flex items-center gap-2 group">
          <div class="w-10 h-10 rounded-xl bg-gradient-to-tr from-emerald-600 to-green-400 flex items-center justify-center font-bold text-lg text-zinc-950 shadow-lg shadow-emerald-500/20 group-hover:scale-105 transition-transform duration-300">
            zz
          </div>
          <span class="text-2xl font-bold tracking-tight text-white group-hover:opacity-90 transition-opacity">
            Pay<span class="text-emerald-500 font-extrabold">.</span>
          </span>
        </a>

        <!-- Menu Links (Desktop) -->
        <div class="hidden md:flex items-center gap-8">
          <a href="#functies" class="text-zinc-400 hover:text-zinc-100 font-medium transition-colors">Hoe het werkt</a>
          <a href="#tarieven" class="text-zinc-400 hover:text-zinc-100 font-medium transition-colors">Tarieven</a>
          <a href="#faq" class="text-zinc-400 hover:text-zinc-100 font-medium transition-colors">Veelgestelde vragen</a>
        </div>

        <!-- Call to Actions -->
        <div class="flex items-center gap-4">
          <a 
            href="https://mijn.zzpay.app/login" 
            class="text-zinc-300 hover:text-white font-medium px-4 py-2 rounded-lg hover:bg-zinc-900 transition-colors duration-300"
          >
            Inloggen
          </a>
          <a 
            href="https://mijn.zzpay.app/register" 
            class="bg-white hover:bg-zinc-100 text-zinc-950 font-semibold px-5 py-2.5 rounded-xl transition-all duration-300 hover:shadow-lg hover:shadow-white/10 active:scale-98"
          >
            Start gratis
          </a>
        </div>
      </nav>
    </header>

    <!-- Main Hero Section -->
    <main class="relative z-10">
      <section class="max-w-7xl mx-auto px-6 pt-20 pb-32 flex flex-col items-center text-center">
        
        <!-- Live status badge -->
        <div ref="heroBadge" class="opacity-0 mb-6 flex items-center gap-2 px-3 py-1.5 rounded-full border border-emerald-500/30 bg-emerald-500/5 text-emerald-400 text-sm font-medium">
          <span class="w-1.5 h-1.5 rounded-full bg-emerald-500 animate-ping"></span>
          <span>Binnen 24 uur je facturen uitbetaald</span>
        </div>

        <!-- Hero Title -->
        <h1 
          ref="heroTitle" 
          class="opacity-0 text-5xl md:text-7xl font-extrabold tracking-tight text-white max-w-4xl leading-tight md:leading-[1.1] text-balance mb-8"
        >
          De slimme betaalstroom voor <span class="bg-gradient-to-r from-emerald-400 to-green-300 bg-clip-text text-transparent">freelancers</span>
        </h1>

        <!-- Hero Subtitle -->
        <p 
          ref="heroSub" 
          class="opacity-0 text-lg md:text-xl text-zinc-400 max-w-2xl text-pretty mb-12"
        >
          Ontvang betalingen sneller, verstuur automatische herinneringen en beheer je geldstroom zonder gedoe. Gekoppeld aan je favoriete bank of boekhoudpakket.
        </p>

        <!-- CTA Buttons -->
        <div 
          ref="heroCtas" 
          class="opacity-0 flex flex-col sm:flex-row items-center gap-4 mb-20 w-full justify-center"
        >
          <a 
            href="https://mijn.zzpay.app/register" 
            class="w-full sm:w-auto bg-gradient-to-r from-emerald-500 to-green-400 hover:from-emerald-600 hover:to-green-500 text-zinc-950 font-bold px-8 py-4 rounded-xl shadow-lg shadow-emerald-500/10 hover:shadow-emerald-500/25 transition-all duration-300 text-center active:scale-98"
          >
            Start gratis proefperiode
          </a>
          <a 
            href="#functies" 
            class="w-full sm:w-auto border border-zinc-800 hover:border-zinc-700 bg-zinc-900/50 hover:bg-zinc-900 text-white font-medium px-8 py-4 rounded-xl transition-all duration-300 text-center"
          >
            Bekijk hoe het werkt
          </a>
        </div>

        <!-- Dashboard Mockup (Hero Visual) -->
        <div 
          ref="heroVisual" 
          class="opacity-0 w-full max-w-5xl relative mt-8 select-none"
        >
          <!-- Outer border decoration -->
          <div class="absolute -inset-1.5 bg-gradient-to-r from-emerald-500/20 to-green-500/20 rounded-2xl blur-lg opacity-40"></div>

          <!-- Main Dashboard Mockup Box -->
          <div class="relative bg-zinc-900/90 border border-zinc-800 rounded-2xl overflow-hidden shadow-2xl backdrop-blur-xl">
            <!-- Window header -->
            <div class="h-12 border-b border-zinc-800/80 bg-zinc-950/50 px-6 flex items-center justify-between">
              <div class="flex items-center gap-2">
                <div class="w-3 h-3 rounded-full bg-zinc-800"></div>
                <div class="w-3 h-3 rounded-full bg-zinc-800"></div>
                <div class="w-3 h-3 rounded-full bg-zinc-800"></div>
              </div>
              <div class="text-xs text-zinc-500 font-mono">mijn.zzpay.app/dashboard</div>
              <div class="w-12"></div>
            </div>

            <!-- Content Area -->
            <div class="p-6 md:p-8 text-left grid grid-cols-1 md:grid-cols-3 gap-6">
              
              <!-- Metric 1 -->
              <div class="bg-zinc-950/60 border border-zinc-800/80 rounded-xl p-6">
                <span class="text-xs font-semibold uppercase tracking-wider text-zinc-500">Gefactureerd deze maand</span>
                <div class="text-3xl font-extrabold text-white mt-2">€ 4.850,00</div>
                <div class="flex items-center gap-2 mt-4 text-emerald-400 text-xs font-medium">
                  <span>+12.4%</span>
                  <span class="text-zinc-500">t.o.v. vorige maand</span>
                </div>
              </div>

              <!-- Metric 2 -->
              <div class="bg-zinc-950/60 border border-zinc-800/80 rounded-xl p-6">
                <span class="text-xs font-semibold uppercase tracking-wider text-zinc-500">Openstaand saldo</span>
                <div class="text-3xl font-extrabold text-white mt-2">€ 1.200,00</div>
                <div class="flex items-center gap-2 mt-4 text-zinc-500 text-xs">
                  <span>2 facturen • Gem. 12 dgn open</span>
                </div>
              </div>

              <!-- Metric 3 -->
              <div class="bg-zinc-950/60 border border-zinc-800/80 rounded-xl p-6 relative overflow-hidden">
                <div class="absolute top-0 right-0 w-24 h-24 bg-emerald-500/10 rounded-full blur-xl"></div>
                <span class="text-xs font-semibold uppercase tracking-wider text-zinc-500">Binnen 24u uitbetaald</span>
                <div class="text-3xl font-extrabold text-emerald-400 mt-2">€ 3.650,00</div>
                <div class="flex items-center gap-2 mt-4 text-emerald-500 text-xs font-semibold">
                  <span class="flex h-2 w-2 relative">
                    <span class="animate-ping absolute inline-flex h-full w-full rounded-full bg-emerald-400 opacity-75"></span>
                    <span class="relative inline-flex rounded-full h-2 w-2 bg-emerald-500"></span>
                  </span>
                  <span>Directe uitbetaling actief ⚡</span>
                </div>
              </div>

              <!-- Detailed Table Mock -->
              <div class="col-span-1 md:col-span-3 bg-zinc-950/60 border border-zinc-800/80 rounded-xl p-6">
                <div class="flex items-center justify-between mb-6">
                  <h3 class="text-base font-bold text-white">Recente Facturen</h3>
                  <a href="#" class="text-xs text-emerald-400 hover:text-emerald-300 font-medium transition-colors">Beheer alles →</a>
                </div>
                <div class="space-y-4">
                  <div class="flex flex-col sm:flex-row sm:items-center justify-between border-b border-zinc-900 pb-4 gap-2">
                    <div>
                      <div class="font-semibold text-sm text-white">Factuur #2026-0048</div>
                      <div class="text-xs text-zinc-500">Opdrachtgever: Acme Corporation</div>
                    </div>
                    <div class="flex items-center justify-between sm:justify-end gap-4">
                      <div class="text-sm font-semibold text-white">€ 1.450,00</div>
                      <span class="px-2.5 py-0.5 rounded-full bg-emerald-500/10 text-emerald-400 text-xs font-semibold border border-emerald-500/20">Betaald via Instant-Pay ⚡</span>
                    </div>
                  </div>
                  <div class="flex flex-col sm:flex-row sm:items-center justify-between border-b border-zinc-900 pb-4 gap-2">
                    <div>
                      <div class="font-semibold text-sm text-white">Factuur #2026-0047</div>
                      <div class="text-xs text-zinc-500">Opdrachtgever: Creative Agency</div>
                    </div>
                    <div class="flex items-center justify-between sm:justify-end gap-4">
                      <div class="text-sm font-semibold text-white">€ 2.200,00</div>
                      <span class="px-2.5 py-0.5 rounded-full bg-emerald-500/10 text-emerald-400 text-xs font-semibold border border-emerald-500/20">Betaald</span>
                    </div>
                  </div>
                  <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-2">
                    <div>
                      <div class="font-semibold text-sm text-white">Factuur #2026-0049</div>
                      <div class="text-xs text-zinc-500">Opdrachtgever: Tech Venture NL</div>
                    </div>
                    <div class="flex items-center justify-between sm:justify-end gap-4">
                      <div class="text-sm font-semibold text-white">€ 1.200,00</div>
                      <span class="px-2.5 py-0.5 rounded-full bg-yellow-500/10 text-yellow-400 text-xs font-semibold border border-yellow-500/20">Herinnering gestuurd</span>
                    </div>
                  </div>
                </div>
              </div>

            </div>
          </div>

          <!-- Floating card 1 -->
          <div class="float-element-1 absolute -top-8 -right-6 md:-right-12 w-64 bg-zinc-900 border border-zinc-800 rounded-xl p-4 shadow-xl backdrop-blur-xl hidden sm:flex items-center gap-3">
            <div class="w-10 h-10 rounded-full bg-emerald-500/25 flex items-center justify-center text-emerald-400 font-extrabold text-sm shadow-inner">
              ✓
            </div>
            <div>
              <div class="text-xs text-zinc-400 font-medium">Factuur betaald!</div>
              <div class="text-sm font-bold text-white">€ 850,00 ontvangen</div>
            </div>
          </div>

          <!-- Floating card 2 -->
          <div class="float-element-2 absolute -bottom-6 -left-6 md:-left-12 w-60 bg-zinc-900 border border-zinc-800 rounded-xl p-4 shadow-xl backdrop-blur-xl hidden sm:flex items-center gap-3">
            <div class="w-10 h-10 rounded-full bg-blue-500/20 flex items-center justify-center text-blue-400 font-bold text-lg">
              ⚡
            </div>
            <div>
              <div class="text-xs text-zinc-400 font-medium">Snelle uitbetaling</div>
              <div class="text-sm font-bold text-white">Verwerkt binnen 2 uur</div>
            </div>
          </div>
        </div>

      </section>

      <!-- Features Section -->
      <section id="functies" class="py-24 bg-zinc-950 border-t border-zinc-900 relative">
        <div class="max-w-7xl mx-auto px-6">
          <div class="text-center max-w-3xl mx-auto mb-16">
            <h2 class="text-xs font-bold uppercase tracking-widest text-emerald-500 mb-3">Waarom ZZPay?</h2>
            <h3 class="text-3xl md:text-4xl font-extrabold text-white text-balance">Alles wat je nodig hebt om je cashflow te versnellen</h3>
          </div>

          <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
            <!-- Feature 1 -->
            <div class="bg-zinc-900/40 border border-zinc-800/80 rounded-2xl p-8 hover:border-zinc-700/80 transition-all duration-300">
              <div class="w-12 h-12 rounded-xl bg-emerald-500/10 border border-emerald-500/20 flex items-center justify-center text-xl mb-6">
                ⚡
              </div>
              <h4 class="text-xl font-bold text-white mb-3">Directe Uitbetaling</h4>
              <p class="text-zinc-400 text-pretty text-sm leading-relaxed">
                Wacht niet langer 30 of 60 dagen op je geld. Met één klik betalen wij je goedgekeurde factuur binnen 24 uur uit.
              </p>
            </div>

            <!-- Feature 2 -->
            <div class="bg-zinc-900/40 border border-zinc-800/80 rounded-2xl p-8 hover:border-zinc-700/80 transition-all duration-300">
              <div class="w-12 h-12 rounded-xl bg-emerald-500/10 border border-emerald-500/20 flex items-center justify-center text-xl mb-6">
                🔔
              </div>
              <h4 class="text-xl font-bold text-white mb-3">Slimme Herinneringen</h4>
              <p class="text-zinc-400 text-pretty text-sm leading-relaxed">
                Automatische, vriendelijke herinneringen per mail of sms wanneer een factuur de vervaldatum nadert. Geen ongemakkelijke telefoontjes meer.
              </p>
            </div>

            <!-- Feature 3 -->
            <div class="bg-zinc-900/40 border border-zinc-800/80 rounded-2xl p-8 hover:border-zinc-700/80 transition-all duration-300">
              <div class="w-12 h-12 rounded-xl bg-emerald-500/10 border border-emerald-500/20 flex items-center justify-center text-xl mb-6">
                🔌
              </div>
              <h4 class="text-xl font-bold text-white mb-3">Simpele Bankkoppeling</h4>
              <p class="text-zinc-400 text-pretty text-sm leading-relaxed">
                Koppel veilig je bankrekening (PSD2) en je boekhoudpakket. Facturen worden automatisch gematcht zodra het geld binnenkomt.
              </p>
            </div>
          </div>
        </div>
      </section>

      <!-- Footer CTA Section -->
      <section class="py-24 bg-zinc-950 relative overflow-hidden border-t border-zinc-900">
        <div class="absolute inset-0 pointer-events-none opacity-20">
          <div class="absolute bottom-0 left-1/2 -translate-x-1/2 w-[600px] h-[300px] rounded-full bg-emerald-500/10 blur-[100px]"></div>
        </div>
        <div class="max-w-4xl mx-auto px-6 text-center relative z-10">
          <h2 class="text-3xl md:text-5xl font-extrabold text-white mb-6 tracking-tight text-balance">Klaar om sneller betaald te krijgen?</h2>
          <p class="text-zinc-400 text-lg mb-10 max-w-xl mx-auto text-pretty">
            Meld je vandaag nog gratis aan en ervaar de vrijheid van een gezonde cashflow. Geen opstartkosten, maandelijks opzegbaar.
          </p>
          <a 
            href="https://mijn.zzpay.app/register" 
            class="inline-block bg-white hover:bg-zinc-100 text-zinc-950 font-bold px-8 py-4 rounded-xl shadow-xl transition-all duration-300 hover:shadow-white/5 hover:scale-103 active:scale-98"
          >
            Maak je gratis account aan
          </a>
        </div>
      </section>
    </main>

    <!-- Footer -->
    <footer class="border-t border-zinc-900 bg-zinc-950 py-12 text-zinc-500 text-sm">
      <div class="max-w-7xl mx-auto px-6 flex flex-col md:flex-row items-center justify-between gap-6">
        <div class="flex items-center gap-2">
          <div class="w-8 h-8 rounded-lg bg-gradient-to-tr from-emerald-600 to-green-400 flex items-center justify-center font-bold text-sm text-zinc-950">
            zz
          </div>
          <span class="font-bold text-white tracking-tight">ZZPay.app</span>
        </div>
        <div class="flex items-center gap-6">
          <a href="#" class="hover:text-zinc-300 transition-colors">Privacybeleid</a>
          <a href="#" class="hover:text-zinc-300 transition-colors">Algemene Voorwaarden</a>
          <a href="#" class="hover:text-zinc-300 transition-colors">Contact</a>
        </div>
        <div>
          &copy; 2026 ZZPay. Alle rechten voorbehouden.
        </div>
      </div>
    </footer>
  </div>
</template>
