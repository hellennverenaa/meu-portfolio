<script setup>
import { ref, onMounted, onUnmounted, nextTick } from 'vue'
import { gsap } from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'

import NavBar from './components/NavBar.vue'
import HeroSection from './components/HeroSection.vue'
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
  // ─── HERO: Entrada inicial sequencial ─────────────────────────────────
  const tlHero = gsap.timeline({ defaults: { ease: 'power3.out' } })

  tlHero
    .to('.hero-badge', {
      opacity: 1, visibility: 'visible', y: 0, duration: 0.8
    })
    .to('.hero-title .gs-hidden', {
      opacity: 1, visibility: 'visible', y: 0, duration: 1,
      stagger: 0.12
    }, '-=0.4')
    .to('.hero-sub', {
      opacity: 1, visibility: 'visible', y: 0, duration: 0.8
    }, '-=0.5')
    .to('.hero-buttons', {
      opacity: 1, visibility: 'visible', y: 0, duration: 0.8
    }, '-=0.4')
    .to('.hero-photo', {
      opacity: 1, visibility: 'visible', scale: 1, duration: 1
    }, '-=0.6')

  // Preparar estados iniciais do hero
  gsap.set('.hero-badge', { opacity: 0, y: 20 })
  gsap.set('.hero-title .gs-hidden', { opacity: 0, y: 60 })
  gsap.set('.hero-sub', { opacity: 0, y: 30 })
  gsap.set('.hero-buttons', { opacity: 0, y: 30 })
  gsap.set('.hero-photo', { opacity: 0, scale: 0.9 })

  // Iniciar a timeline
  tlHero.play()

  // ─── PROJETOS: Revelação com scroll ───────────────────────────────────
  gsap.utils.toArray('.projeto-label, .projeto-title, .projeto-desc').forEach(el => {
    gsap.set(el, { opacity: 0, y: 40 })
    gsap.to(el, {
      scrollTrigger: {
        trigger: el,
        start: 'top 85%',
        toggleActions: 'play none none none',
      },
      opacity: 1, visibility: 'visible', y: 0,
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
      opacity: 1, visibility: 'visible', y: 0,
      duration: 0.9, ease: 'power3.out',
      delay: i * 0.1
    })
  })

  // ─── TIMELINE (CARREIRA): Scrollytelling com scrub ────────────────────
  // Fio cresce com o scroll
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

  // Cabeçalho da timeline
  gsap.utils.toArray('.timeline-label, .timeline-title').forEach(el => {
    gsap.set(el, { opacity: 0, y: 40 })
    gsap.to(el, {
      scrollTrigger: {
        trigger: el,
        start: 'top 85%',
        toggleActions: 'play none none none',
      },
      opacity: 1, visibility: 'visible', y: 0,
      duration: 0.8, ease: 'power3.out'
    })
  })

  // Items da timeline — revelação individual
  gsap.utils.toArray('.timeline-item').forEach((el, i) => {
    gsap.set(el, { opacity: 0, x: -40 })
    gsap.to(el, {
      scrollTrigger: {
        trigger: el,
        start: 'top 85%',
        end: 'top 50%',
        scrub: 1,
      },
      opacity: 1, visibility: 'visible', x: 0,
      ease: 'power3.out'
    })
  })

  // ─── SOBRE: Revelação sequencial ──────────────────────────────────────
  gsap.utils.toArray('.sobre-label, .sobre-title, .sobre-text, .sobre-stat, .sobre-comp').forEach((el, i) => {
    gsap.set(el, { opacity: 0, y: 30 })
    gsap.to(el, {
      scrollTrigger: {
        trigger: el,
        start: 'top 88%',
        toggleActions: 'play none none none',
      },
      opacity: 1, visibility: 'visible', y: 0,
      duration: 0.7, ease: 'power3.out',
      delay: (i % 4) * 0.06
    })
  })

  // ─── CONTATO: Revelação ───────────────────────────────────────────────
  gsap.utils.toArray('.contato-label, .contato-title, .contato-text, .contato-cta').forEach((el, i) => {
    gsap.set(el, { opacity: 0, y: 30 })
    gsap.to(el, {
      scrollTrigger: {
        trigger: el,
        start: 'top 88%',
        toggleActions: 'play none none none',
      },
      opacity: 1, visibility: 'visible', y: 0,
      duration: 0.8, ease: 'power3.out',
      delay: i * 0.1
    })
  })
}

// ─── Lifecycle ──────────────────────────────────────────────────────────────
onMounted(() => {
  document.documentElement.classList.add('dark')
  window.addEventListener('scroll', aoRolar, { passive: true })

  nextTick(() => {
    // Pequeno delay para garantir que o DOM está renderizado
    requestAnimationFrame(() => {
      inicializarAnimacoes()
    })
  })
})

onUnmounted(() => {
  window.removeEventListener('scroll', aoRolar)
  ScrollTrigger.getAll().forEach(st => st.kill())
})
</script>

<template>
  <div class="min-h-screen bg-[#0F0E0C] text-[#EDE8DF] antialiased">
    <NavBar :scrollY="scrollY" />
    <HeroSection />
    <MarqueeBand />
    <ProjetosSection />
    <TimelineSection />
    <ContatoSection />
  </div>
</template>
