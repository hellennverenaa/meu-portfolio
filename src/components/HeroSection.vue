<template>
  <section id="inicio" class="hero-section relative min-h-screen flex flex-col justify-between pt-28 pb-12 px-6 max-w-7xl mx-auto z-10 overflow-hidden">
    <canvas ref="particleCanvas" class="absolute inset-0 pointer-events-none z-0"></canvas>

    <div class="grid grid-cols-1 lg:grid-cols-12 gap-12 items-center z-10 w-full my-auto">

      <!-- Tipografia + CTAs -->
      <div class="lg:col-span-7 flex flex-col text-left">
        <div class="hero-badge opacity-0 inline-flex items-center gap-2 px-3 py-1 rounded-full border border-[var(--color-ultraviolet)]/30 bg-[var(--color-bg-surface)]/50 text-xs font-mono text-[var(--color-magenta)] mb-6 w-fit backdrop-blur-md">
          <span class="w-2 h-2 rounded-full bg-[var(--color-terminal)] animate-pulse"></span>
          ARQUITETURA DE SOFTWARE & SOLUÇÕES INDUSTRIAIS
        </div>

        <h1 class="hero-title text-6xl md:text-8xl font-black text-[var(--color-text-pure)] leading-none tracking-brutal uppercase select-none overflow-hidden">
          <span class="gs-hidden block opacity-0 transform translate-y-full">HELLEN</span>
          <span class="gs-hidden block opacity-0 transform translate-y-full text-transparent bg-clip-text bg-gradient-to-r from-[var(--color-ultraviolet)] to-[var(--color-magenta)]">VERENA</span>
        </h1>

        <p class="hero-sub opacity-0 mt-8 text-lg md:text-xl text-[var(--color-text-muted)] max-w-xl font-normal leading-relaxed">
          Especialista em otimização extrema de <span class="text-[var(--color-text-pure)] font-mono">PostgreSQL</span> e arquitetura com <span class="text-[var(--color-text-pure)] font-mono">Prisma ORM</span>. Desenvolvendo sistemas inteligentes de alta performance para o chão de fábrica industrial.
        </p>

        <div class="hero-buttons opacity-0 mt-10 flex flex-wrap gap-4">
          <a href="#projetos" class="group relative px-8 py-4 bg-[var(--color-ultraviolet)] hover:bg-[var(--color-magenta)] text-white font-medium rounded-full transition-all duration-500 ease-[cubic-bezier(0.32,0.72,0,1)] transform-gpu hover:scale-105 shadow-[0_0_25px_rgba(112,0,255,0.4)] hover:shadow-[0_0_30px_rgba(255,0,127,0.6)] active:scale-95 focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-[var(--color-magenta)]/50">
            Ver Projetos Ativos
          </a>
          <a href="#contato" class="px-8 py-4 rounded-full border border-[var(--color-border)] hover:border-[var(--color-magenta)] bg-[var(--color-bg-surface)]/40 text-[var(--color-text-pure)] font-medium transition-all duration-300 backdrop-blur-md active:scale-95 focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-[var(--color-ultraviolet)]/50">
            Iniciar Conexão
          </a>
        </div>
      </div>

      <!-- Crachá Flutuante (ÚNICO elemento visual nesta seção) -->
      <div class="lg:col-span-5 flex justify-center lg:justify-end relative min-h-[480px] w-full">
        <div ref="avatarContainer" class="hero-photo relative w-80 h-[450px] flex items-center justify-center">
          <div
            ref="floatingCard"
            class="floating-card absolute w-72 h-96 bg-[var(--color-bg-surface)]/80 border border-[var(--color-ultraviolet)]/40 rounded-2xl p-4 shadow-[0_0_50px_rgba(112,0,255,0.15)] backdrop-blur-xl flex flex-col justify-between transition-transform duration-300 pointer-events-auto transform-gpu will-change-transform"
          >
            <!-- Câmera / Notch -->
            <div class="w-full flex justify-between items-center border-b border-[var(--color-border)] pb-3">
              <div class="w-12 h-3 bg-zinc-800 rounded-full mx-auto relative shadow-inner">
                <div class="absolute inset-x-3 top-0 h-1 bg-zinc-700 rounded-full"></div>
              </div>
            </div>

            <!-- Foto com Blob Morph -->
            <div class="relative w-full aspect-square my-auto overflow-hidden bg-gradient-to-tr from-[var(--color-ultraviolet)] to-[var(--color-magenta)] p-[2px] animate-blob-morph">
              <div class="w-full h-full bg-[var(--color-bg-main)] animate-blob-morph overflow-hidden">
                <img src="../assets/hero.png" alt="Hellen Verena" class="w-full h-full object-cover mix-blend-luminosity hover:mix-blend-normal transition-all duration-700 scale-105" />
              </div>
            </div>

            <!-- Código de barras / ID -->
            <div class="border-t border-[var(--color-border)] pt-3 flex flex-col items-center gap-1 font-mono">
              <span class="text-[10px] text-[var(--color-text-muted)] tracking-widest">SST_H_MAGALHAES_2026</span>
              <div class="w-full h-6 bg-[var(--color-text-pure)] opacity-10 rounded-sm mt-1 flex gap-[2px] p-1 overflow-hidden">
                <div class="h-full bg-white w-1"></div><div class="h-full bg-white w-[2px]"></div><div class="h-full bg-white w-1"></div><div class="h-full bg-white w-[3px]"></div><div class="h-full bg-white w-[1px]"></div><div class="h-full bg-white w-2"></div><div class="h-full bg-white w-[2px]"></div><div class="h-full bg-white w-1"></div><div class="h-full bg-white w-[3px]"></div><div class="h-full bg-white w-1"></div>
              </div>
            </div>
          </div>
        </div>
      </div>

    </div>

    <!-- Barra inferior -->
    <div class="hero-footer opacity-0 w-full flex justify-between items-center font-mono text-xs text-[var(--color-text-muted)] border-t border-[var(--color-border)] pt-6 mt-12 z-10">
      <div class="flex items-center gap-4">
        <span>[ SCALE ] ATIVO</span>
        <span>[ SOBRACORTE ] CORE</span>
      </div>
      <div class="animate-bounce text-[var(--color-magenta)]">
        ↓ ROLAR PARA EXPLORAR
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import { gsap } from 'gsap'

// Referências do Template
const particleCanvas = ref(null)
const floatingCard = ref(null)
const avatarContainer = ref(null)

let animationFrameId = null

// ─── Efeito Magnético no Crachá (Segue levemente o mouse) ──────────────────
const aplicarEfeitoMagnetico = (e) => {
  if (window.scrollY > 200) return
  const card = floatingCard.value
  if (!card) return
  const bounds = card.getBoundingClientRect()
  const mouseX = e.clientX - bounds.left - bounds.width / 2
  const mouseY = e.clientY - bounds.top - bounds.height / 2

  gsap.to(card, {
    x: mouseX * 0.15,
    y: mouseY * 0.15,
    rotationY: mouseX * 0.05,
    rotationX: -mouseY * 0.05,
    duration: 0.5,
    ease: "power2.out"
  })
}

const resetarEfeitoMagnetico = () => {
  if (!floatingCard.value) return
  gsap.to(floatingCard.value, {
    x: 0, y: 0,
    rotationX: 0, rotationY: 0,
    duration: 0.8,
    ease: "power3.out"
  })
}

onMounted(() => {
  window.addEventListener('mousemove', aplicarEfeitoMagnetico)
  window.addEventListener('mouseleave', resetarEfeitoMagnetico)

  // ─── Canvas de Partículas (Ultravioleta & Magenta) ──────────────────────
  const canvas = particleCanvas.value
  if (!canvas) return
  const ctx = canvas.getContext('2d')

  const redimensionar = () => {
    canvas.width = canvas.parentElement.offsetWidth
    canvas.height = canvas.parentElement.offsetHeight
  }
  redimensionar()
  window.addEventListener('resize', redimensionar)

  const particulas = []
  const quantidade = 40

  for (let i = 0; i < quantidade; i++) {
    particulas.push({
      x: Math.random() * canvas.width,
      y: Math.random() * canvas.height,
      radius: Math.random() * 1.5 + 0.5,
      vx: (Math.random() - 0.5) * 0.3,
      vy: (Math.random() - 0.5) * 0.3,
      color: Math.random() > 0.5 ? 'rgba(112, 0, 255, ' : 'rgba(255, 0, 127, '
    })
  }

  const loopAnimacao = () => {
    ctx.clearRect(0, 0, canvas.width, canvas.height)

    particulas.forEach(p => {
      p.x += p.vx
      p.y += p.vy
      if (p.x < 0 || p.x > canvas.width) p.vx *= -1
      if (p.y < 0 || p.y > canvas.height) p.vy *= -1

      ctx.beginPath()
      ctx.arc(p.x, p.y, p.radius, 0, Math.PI * 2)
      ctx.fillStyle = p.color + '0.4)'
      ctx.fill()
    })

    ctx.lineWidth = 0.5
    for (let i = 0; i < particulas.length; i++) {
      for (let j = i + 1; j < particulas.length; j++) {
        const dist = Math.hypot(particulas[i].x - particulas[j].x, particulas[i].y - particulas[j].y)
        if (dist < 140) {
          ctx.beginPath()
          ctx.moveTo(particulas[i].x, particulas[i].y)
          ctx.lineTo(particulas[j].x, particulas[j].y)
          ctx.strokeStyle = `rgba(112, 0, 255, ${(1 - dist / 140) * 0.12})`
          ctx.stroke()
        }
      }
    }

    animationFrameId = requestAnimationFrame(loopAnimacao)
  }
  loopAnimacao()
})

onUnmounted(() => {
  window.removeEventListener('mousemove', aplicarEfeitoMagnetico)
  window.removeEventListener('mouseleave', resetarEfeitoMagnetico)
  cancelAnimationFrame(animationFrameId)
})
</script>