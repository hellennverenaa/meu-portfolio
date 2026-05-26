<script setup>
import { ref, onMounted, onUnmounted, nextTick } from 'vue'
import { gsap } from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'

import NavBar from './components/NavBar.vue'
import HeroSection from './components/HeroSection.vue'
import SobreMimSection from './components/SobreMimSection.vue'
import ServicosSection from './components/ServicosSection.vue'
import MarqueeBand from './components/MarqueeBand.vue'
import ProjetosSection from './components/ProjetosSection.vue'
import TimelineSection from './components/TimelineSection.vue'
import ContatoSection from './components/ContatoSection.vue'

// ─── Registrar plugin GSAP ──────────────────────────────────────────────────
gsap.registerPlugin(ScrollTrigger)

// ─── Scroll tracking para a NavBar ──────────────────────────────────────────
const scrollY = ref(0)

function aoRolar() {
  scrollY.value = window.scrollY
}

// ─── Motor de Animação GSAP — Scrollytelling ────────────────────────────────
function inicializarAnimacoes() {

  // ═══════════════════════════════════════════════════════════════════════════
  // 1. HERO: Entrada inicial sequencial (o crachá tem sua própria animação)
  // ═══════════════════════════════════════════════════════════════════════════
  gsap.set('.hero-badge', { opacity: 0, y: 20 })
  gsap.set('.hero-title .gs-hidden', { opacity: 0, y: 60 })
  gsap.set('.hero-sub', { opacity: 0, y: 30 })
  gsap.set('.hero-buttons', { opacity: 0, y: 30 })
  gsap.set('.hero-footer', { opacity: 0, y: 20 })

  const tlHero = gsap.timeline({ defaults: { ease: 'power3.out' } })

  tlHero
    .to('.hero-badge', { opacity: 1, y: 0, duration: 0.8 })
    .to('.hero-title .gs-hidden', {
      opacity: 1, y: 0, duration: 1, stagger: 0.12
    }, '-=0.4')
    .to('.hero-sub', { opacity: 1, y: 0, duration: 0.8 }, '-=0.5')
    .to('.hero-buttons', { opacity: 1, y: 0, duration: 0.8 }, '-=0.4')
    .to('.hero-footer', { opacity: 1, y: 0, duration: 0.6 }, '-=0.3')

  // ═══════════════════════════════════════════════════════════════════════════
  // 2. A GRANDE TRANSIÇÃO: Hero → Sobre Mim (ScrollTrigger)
  //    O crachá e o cordão desaparecem ao rolar
  // ═══════════════════════════════════════════════════════════════════════════
  const floatingCard = document.querySelector('.floating-card')
  const cordSvg = document.querySelector('.hero-section svg')
  if (floatingCard) {
    gsap.to(floatingCard, {
      scrollTrigger: {
        trigger: '.hero-section',
        start: 'top top',
        end: '+=500',
        scrub: 1,
      },
      opacity: 0,
      scale: 0.8,
      y: -50,
      ease: 'none'
    })
  }
  if (cordSvg) {
    gsap.to(cordSvg, {
      scrollTrigger: {
        trigger: '.hero-section',
        start: 'top top',
        end: '+=400',
        scrub: 1,
      },
      opacity: 0,
      ease: 'none'
    })
  }

  // ═══════════════════════════════════════════════════════════════════════════
  // 3. SOBRE MIM: Revelação sequencial com scroll
  // ═══════════════════════════════════════════════════════════════════════════
  gsap.utils.toArray('.sobre-label, .sobre-title').forEach(el => {
    gsap.set(el, { opacity: 0, y: 40 })
    gsap.to(el, {
      scrollTrigger: {
        trigger: el,
        start: 'top 85%',
        toggleActions: 'play none none none',
      },
      opacity: 1, y: 0,
      duration: 0.8, ease: 'power3.out'
    })
  })

  gsap.utils.toArray('.sobre-text, .sobre-stat, .sobre-comp, .sobre-photo').forEach((el, i) => {
    gsap.set(el, { opacity: 0, y: 30 })
    gsap.to(el, {
      scrollTrigger: {
        trigger: el,
        start: 'top 88%',
        toggleActions: 'play none none none',
      },
      opacity: 1, y: 0,
      duration: 0.7, ease: 'power3.out',
      delay: (i % 4) * 0.06
    })
  })

  // ═══════════════════════════════════════════════════════════════════════════
  // 4. SERVIÇOS: Cards com stagger
  // ═══════════════════════════════════════════════════════════════════════════
  gsap.utils.toArray('.servico-label, .servico-title, .servico-desc').forEach(el => {
    gsap.set(el, { opacity: 0, y: 40 })
    gsap.to(el, {
      scrollTrigger: {
        trigger: el,
        start: 'top 85%',
        toggleActions: 'play none none none',
      },
      opacity: 1, y: 0,
      duration: 0.8, ease: 'power3.out'
    })
  })

  gsap.utils.toArray('.servico-card').forEach((el, i) => {
    gsap.set(el, { opacity: 0, y: 50 })
    gsap.to(el, {
      scrollTrigger: {
        trigger: el,
        start: 'top 88%',
        toggleActions: 'play none none none',
      },
      opacity: 1, y: 0,
      duration: 0.9, ease: 'power3.out',
      delay: i * 0.15
    })
  })

  // ═══════════════════════════════════════════════════════════════════════════
  // 5. PROJETOS: Revelação com scroll
  // ═══════════════════════════════════════════════════════════════════════════
  gsap.utils.toArray('.projeto-label, .projeto-title, .projeto-desc').forEach(el => {
    gsap.set(el, { opacity: 0, y: 40 })
    gsap.to(el, {
      scrollTrigger: {
        trigger: el,
        start: 'top 85%',
        toggleActions: 'play none none none',
      },
      opacity: 1, y: 0,
      duration: 0.8, ease: 'power3.out'
    })
  })

  gsap.utils.toArray('.projeto-card').forEach((el, i) => {
    gsap.set(el, { opacity: 0, y: 50 })
    gsap.to(el, {
      scrollTrigger: {
        trigger: el,
        start: 'top 88%',
        toggleActions: 'play none none none',
      },
      opacity: 1, y: 0,
      duration: 0.9, ease: 'power3.out',
      delay: i * 0.1
    })
  })

  // ═══════════════════════════════════════════════════════════════════════════
  // 6. TIMELINE (CARREIRA): Scrollytelling com scrub
  // ═══════════════════════════════════════════════════════════════════════════
  const timelineLine = document.querySelector('.timeline-line')
  if (timelineLine) {
    gsap.set(timelineLine, { scaleY: 0 })
    gsap.to(timelineLine, {
      scrollTrigger: {
        trigger: '.timeline',
        start: 'top 60%',
        end: 'bottom 40%',
        scrub: 1.5,
      },
      scaleY: 1,
      ease: 'none'
    })
  }

  gsap.utils.toArray('.timeline-label, .timeline-title').forEach(el => {
    gsap.set(el, { opacity: 0, y: 40 })
    gsap.to(el, {
      scrollTrigger: {
        trigger: el,
        start: 'top 85%',
        toggleActions: 'play none none none',
      },
      opacity: 1, y: 0,
      duration: 0.8, ease: 'power3.out'
    })
  })

  gsap.utils.toArray('.timeline-item').forEach((el) => {
    gsap.set(el, { opacity: 0, x: -40 })
    gsap.to(el, {
      scrollTrigger: {
        trigger: el,
        start: 'top 85%',
        end: 'top 50%',
        scrub: 1,
      },
      opacity: 1, x: 0,
      ease: 'power3.out'
    })
  })

  // ═══════════════════════════════════════════════════════════════════════════
  // 7. CONTATO: Revelação sequencial
  // ═══════════════════════════════════════════════════════════════════════════
  gsap.utils.toArray('.contato-label, .contato-title, .contato-text, .contato-cta').forEach((el, i) => {
    gsap.set(el, { opacity: 0, y: 30 })
    gsap.to(el, {
      scrollTrigger: {
        trigger: el,
        start: 'top 88%',
        toggleActions: 'play none none none',
      },
      opacity: 1, y: 0,
      duration: 0.8, ease: 'power3.out',
      delay: i * 0.1
    })
  })
}

// ─── Lifecycle ──────────────────────────────────────────────────────────────
onMounted(() => {
  // Correção de Scroll Restoration (Bug do F5)
  if ('scrollRestoration' in history) {
    history.scrollRestoration = 'manual'
  }
  window.scrollTo(0, 0)

  // O tema dark é definido pelo index.html (<html class="dark">)
  // e controlado pelo NavBar. Não forçamos aqui.
  window.addEventListener('scroll', aoRolar, { passive: true })

  nextTick(() => {
    requestAnimationFrame(() => {
      inicializarAnimacoes()
    })
  })
})

onUnmounted(() => {
  window.removeEventListener('scroll', aoRolar)
  ScrollTrigger.getAll().forEach(st => st.kill())
  gsap.killTweensOf('*')
})
</script>

<template>
  <div class="min-h-screen bg-[var(--color-bg-main)] text-[var(--color-text-pure)] antialiased overflow-x-hidden">
    <NavBar :scrollY="scrollY" />
    <HeroSection />
    <SobreMimSection />
    <ServicosSection />
    <MarqueeBand />
    <ProjetosSection />
    <TimelineSection />
    <ContatoSection />
  </div>
</template>
