<script setup>
import { ref, onMounted, onUnmounted, nextTick } from 'vue'
import { gsap } from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'
import { ScrollToPlugin } from 'gsap/ScrollToPlugin'

// ─── Registrar plugins GSAP ──────────────────────────────────────────────────
gsap.registerPlugin(ScrollTrigger, ScrollToPlugin)

import NavBar from './components/NavBar.vue'
import HeroSection from './components/HeroSection.vue'
import SobreMimSection from './components/SobreMimSection.vue'
import ServicosSection from './components/ServicosSection.vue'
import MarqueeBand from './components/MarqueeBand.vue'
import ProjetosSection from './components/ProjetosSection.vue'
import TimelineSection from './components/TimelineSection.vue'
import StacksSection from './components/StacksSection.vue'
import ContatoSection from './components/ContatoSection.vue'

// ─── Registrar plugin GSAP ──────────────────────────────────────────────────
gsap.registerPlugin(ScrollTrigger)

// ─── Scroll tracking para a NavBar ──────────────────────────────────────────
const scrollY = ref(0)
const heroPinWrapper = ref(null) // <--- ÂNCORA INFALÍVEL DO VUE PARA O GSAP

function aoRolar() {
  scrollY.value = window.scrollY
}

// ─── Motor de Animação GSAP — Scrollytelling ────────────────────────────────
function inicializarAnimacoes() {

  // 1. HERO: Entrada inicial — elementos individuais aparecem em sequência
  gsap.set('.hero-badge', { opacity: 0, y: 20 })
  gsap.set('.hero-avail-badge', { opacity: 0, y: -10 })
  gsap.set('.hero-title .gs-hidden', { opacity: 0, y: 60 })
  gsap.set('.hero-sub', { opacity: 0, y: 30 })
  gsap.set('.hero-buttons', { opacity: 0, y: 30 })
  gsap.set('.hero-stacks', { opacity: 0, y: 20 })
  gsap.set('.hero-footer', { opacity: 0, y: 20 })

  const tlHero = gsap.timeline({ defaults: { ease: 'power3.out' } })

  tlHero
    .to('.hero-badge', { opacity: 1, y: 0, duration: 0.8 })
    .to('.hero-avail-badge', { opacity: 1, y: 0, duration: 0.6 }, '-=0.4')
    .to('.hero-title .gs-hidden', { opacity: 1, y: 0, duration: 1, stagger: 0.12 }, '-=0.4')
    .to('.hero-sub', { opacity: 1, y: 0, duration: 0.8 }, '-=0.5')
    .to('.hero-buttons', { opacity: 1, y: 0, duration: 0.8 }, '-=0.4')
    .to('.hero-stacks', { opacity: 1, y: 0, duration: 0.7 }, '-=0.3')
    .to('.hero-footer', { opacity: 1, y: 0, duration: 0.6 }, '-=0.3')

  // ═══════════════════════════════════════════════════════════════════════════
  // 2. A GRANDE TRANSIÇÃO — Pin + Fade-out da seção inteira
  //
  //    Animamos APENAS o wrapper .hero-fade-wrapper (container pai),
  //    que começa com opacity:1 (nunca é tocado pelo tlHero). Assim o scrub
  //    reverso restaura para opacity:1 corretamente, e todos os filhos
  //    reaparecem junto.
  // ═══════════════════════════════════════════════════════════════════════════
  if (heroPinWrapper.value) {
    const tlPin = gsap.timeline({
      scrollTrigger: {
        trigger: heroPinWrapper.value,
        start: 'top top',
        end: () => window.innerHeight,
        pin: true,
        pinSpacing: false,
        scrub: 1,
        invalidateOnRefresh: true,
      }
    })

    // Anima o wrapper que envolve TODO o conteúdo da hero-section.
    // Dura apenas 0.4 do scroll total para que a Hero apague rapidamente enquanto a próxima seção sobe.
    tlPin.to('.hero-fade-wrapper', { opacity: 0, y: -40, duration: 0.4 }, 0)
  }

  // 3. SOBRE MIM
  gsap.utils.toArray('.sobre-label, .sobre-title').forEach(el => {
    gsap.set(el, { opacity: 0, y: 40 })
    gsap.to(el, { scrollTrigger: { trigger: el, start: 'top 85%', toggleActions: 'play none none none' }, opacity: 1, y: 0, duration: 0.8, ease: 'power3.out' })
  })

  gsap.utils.toArray('.sobre-text, .sobre-stat, .sobre-comp, .sobre-photo').forEach((el, i) => {
    gsap.set(el, { opacity: 0, y: 30 })
    gsap.to(el, { scrollTrigger: { trigger: el, start: 'top 88%', toggleActions: 'play none none none' }, opacity: 1, y: 0, duration: 0.7, ease: 'power3.out', delay: (i % 4) * 0.06 })
  })

  // 4. SERVIÇOS
  gsap.utils.toArray('.servico-label, .servico-title, .servico-desc').forEach(el => {
    gsap.set(el, { opacity: 0, y: 40 })
    gsap.to(el, { scrollTrigger: { trigger: el, start: 'top 85%', toggleActions: 'play none none none' }, opacity: 1, y: 0, duration: 0.8, ease: 'power3.out' })
  })

  gsap.utils.toArray('.servico-card').forEach((el, i) => {
    gsap.set(el, { opacity: 0, y: 50 })
    gsap.to(el, { scrollTrigger: { trigger: el, start: 'top 88%', toggleActions: 'play none none none' }, opacity: 1, y: 0, duration: 0.9, ease: 'power3.out', delay: i * 0.15 })
  })

  // 5. PROJETOS
  gsap.utils.toArray('.projeto-label, .projeto-title, .projeto-desc').forEach(el => {
    gsap.set(el, { opacity: 0, y: 40 })
    gsap.to(el, { scrollTrigger: { trigger: el, start: 'top 85%', toggleActions: 'play none none none' }, opacity: 1, y: 0, duration: 0.8, ease: 'power3.out' })
  })

  gsap.utils.toArray('.projeto-card').forEach((el, i) => {
    gsap.set(el, { opacity: 0, y: 50 })
    gsap.to(el, { scrollTrigger: { trigger: el, start: 'top 88%', toggleActions: 'play none none none' }, opacity: 1, y: 0, duration: 0.9, ease: 'power3.out', delay: i * 0.1 })
  })

  // 6. TIMELINE (CARREIRA)
  const timelineLine = document.querySelector('.timeline-line')
  if (timelineLine) {
    gsap.set(timelineLine, { scaleY: 0 })
    gsap.to(timelineLine, { scrollTrigger: { trigger: '.timeline', start: 'top 60%', end: 'bottom 40%', scrub: 1.5 }, scaleY: 1, ease: 'none' })
  }

  gsap.utils.toArray('.timeline-label, .timeline-title').forEach(el => {
    gsap.set(el, { opacity: 0, y: 40 })
    gsap.to(el, { scrollTrigger: { trigger: el, start: 'top 85%', toggleActions: 'play none none none' }, opacity: 1, y: 0, duration: 0.8, ease: 'power3.out' })
  })

  gsap.utils.toArray('.timeline-item').forEach((el) => {
    gsap.set(el, { opacity: 0, x: -40 })
    gsap.to(el, { scrollTrigger: { trigger: el, start: 'top 85%', end: 'top 50%', scrub: 1 }, opacity: 1, x: 0, ease: 'power3.out' })
  })

  // 7. STACKS & FERRAMENTAS
  gsap.utils.toArray('.stacks-label, .stacks-title, .stacks-desc').forEach(el => {
    gsap.set(el, { opacity: 0, y: 40 })
    gsap.to(el, { scrollTrigger: { trigger: el, start: 'top 85%', toggleActions: 'play none none none' }, opacity: 1, y: 0, duration: 0.8, ease: 'power3.out' })
  })

  gsap.utils.toArray('.stacks-card').forEach((el, i) => {
    gsap.set(el, { opacity: 0, y: 50 })
    gsap.to(el, { scrollTrigger: { trigger: el, start: 'top 88%', toggleActions: 'play none none none' }, opacity: 1, y: 0, duration: 0.9, ease: 'power3.out', delay: i * 0.1 })
  })

  // 8. CONTATO
  gsap.utils.toArray('.contato-label, .contato-title, .contato-text, .contato-cta').forEach((el, i) => {
    gsap.set(el, { opacity: 0, y: 30 })
    gsap.to(el, { scrollTrigger: { trigger: el, start: 'top 88%', toggleActions: 'play none none none' }, opacity: 1, y: 0, duration: 0.8, ease: 'power3.out', delay: i * 0.1 })
  })
}

// ─── Lifecycle ──────────────────────────────────────────────────────────────
onMounted(() => {
  if ('scrollRestoration' in history) {
    history.scrollRestoration = 'manual';
  }
  
  setTimeout(() => {
    window.scrollTo(0, 0);
  }, 50);

  window.addEventListener('scroll', aoRolar, { passive: true })

  nextTick(() => {
    setTimeout(() => {
      requestAnimationFrame(() => {
        inicializarAnimacoes()
      })
    }, 100)
  })
})

onUnmounted(() => {
  window.removeEventListener('scroll', aoRolar)
  ScrollTrigger.getAll().forEach(st => st.kill())
  gsap.killTweensOf('*')
})
</script>

<template>
  <div class="bg-[var(--color-bg-main)] text-[var(--color-text-pure)] font-sans min-h-screen">
    <!-- Navbar FORA do main/pin para z-index isolado -->
    <NavBar :scrollY="scrollY" />
    <main class="w-full relative z-10">
      
      <div ref="heroPinWrapper" class="w-full relative">
        <HeroSection />
      </div>
      
      <SobreMimSection />
      <TimelineSection />
      <ServicosSection />
      <MarqueeBand />
      <ProjetosSection />
      <StacksSection />
      <ContatoSection />
      
    </main>
  </div>
</template>