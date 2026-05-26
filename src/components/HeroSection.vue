<template>
  <section id="inicio" class="hero-section relative min-h-screen flex flex-col justify-between pt-24 md:pt-28 pb-8 md:pb-12 px-4 md:px-6 max-w-7xl mx-auto z-10 overflow-visible">
    <canvas ref="particleCanvas" class="absolute inset-0 pointer-events-none z-0"></canvas>

    <!-- SVG Cordão do Crachá -->
    <svg ref="cordSvgRef" class="absolute inset-0 w-full h-full pointer-events-none z-20 overflow-visible">
      <defs>
        <linearGradient id="cordGradient" x1="0%" y1="0%" x2="0%" y2="100%">
          <stop offset="0%" stop-color="var(--color-text-muted)" stop-opacity="0.5" />
          <stop offset="100%" stop-color="var(--color-ultraviolet)" stop-opacity="0.8" />
        </linearGradient>
      </defs>
      <path ref="cordPathRef" fill="none" stroke="url(#cordGradient)" stroke-width="2.5" stroke-linecap="round" />
    </svg>

    <div class="grid grid-cols-1 lg:grid-cols-12 gap-8 md:gap-12 items-center z-10 w-full my-auto">

      <!-- Tipografia + CTAs -->
      <div class="lg:col-span-7 flex flex-col text-left order-2 lg:order-1">
        <div class="hero-badge opacity-0 inline-flex items-center gap-2 px-3 py-1 rounded-full border border-[var(--color-ultraviolet)]/30 bg-[var(--color-bg-surface)]/50 text-xs font-mono text-[var(--color-magenta)] mb-4 md:mb-6 w-fit backdrop-blur-md">
          <span class="w-2 h-2 rounded-full bg-[var(--color-terminal)] animate-pulse"></span>
          ARQUITETURA DE SOFTWARE & SOLUÇÕES INDUSTRIAIS
        </div>

        <h1 class="hero-title text-4xl sm:text-5xl md:text-6xl lg:text-8xl font-black text-[var(--color-text-pure)] leading-none tracking-brutal uppercase select-none overflow-hidden">
          <span class="gs-hidden block opacity-0 transform translate-y-full">HELLEN</span>
          <span class="gs-hidden block opacity-0 transform translate-y-full text-transparent bg-clip-text bg-gradient-to-r from-[var(--color-ultraviolet)] to-[var(--color-magenta)]">VERENA</span>
        </h1>

        <p class="hero-sub opacity-0 mt-6 md:mt-8 text-base md:text-lg lg:text-xl text-[var(--color-text-muted)] max-w-xl font-normal leading-relaxed">
          Especialista em otimização extrema de <span class="text-[var(--color-text-pure)] font-mono">PostgreSQL</span> e arquitetura com <span class="text-[var(--color-text-pure)] font-mono">Prisma ORM</span>. Desenvolvendo sistemas inteligentes de alta performance para o chão de fábrica industrial.
        </p>

        <div class="hero-buttons opacity-0 mt-8 md:mt-10 flex flex-wrap gap-3 md:gap-4">
          <a href="#projetos" class="group relative px-6 md:px-8 py-3 md:py-4 bg-[var(--color-ultraviolet)] hover:bg-[var(--color-magenta)] text-white font-medium rounded-full transition-all duration-500 ease-[cubic-bezier(0.32,0.72,0,1)] transform-gpu hover:scale-105 shadow-[0_0_25px_rgba(112,0,255,0.4)] hover:shadow-[0_0_30px_rgba(255,0,127,0.6)] active:scale-95 focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-[var(--color-magenta)]/50 text-sm md:text-base">
            Ver Projetos Ativos
          </a>
          <a href="#contato" class="px-6 md:px-8 py-3 md:py-4 rounded-full border border-[var(--color-border)] hover:border-[var(--color-magenta)] bg-[var(--color-bg-surface)]/40 text-[var(--color-text-pure)] font-medium transition-all duration-300 backdrop-blur-md active:scale-95 focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-[var(--color-ultraviolet)]/50 text-sm md:text-base">
            Iniciar Conexão
          </a>
        </div>
      </div>

      <!-- Crachá Flutuante — Pendurado por Cordão com Drag & Throw -->
      <div class="lg:col-span-5 flex justify-center lg:justify-end relative min-h-[320px] md:min-h-[480px] w-full order-1 lg:order-2">
        <div ref="badgeContainer" class="badge-container relative w-56 md:w-72 lg:w-80 flex items-start justify-center pt-8 md:pt-0">
          <div
            ref="badgeRef"
            class="hero-photo floating-card relative w-48 md:w-64 lg:w-72 bg-[var(--color-bg-surface)]/80 border border-[var(--color-ultraviolet)]/40 rounded-2xl shadow-[0_0_50px_rgba(112,0,255,0.15)] backdrop-blur-xl flex flex-col transition-shadow duration-300 pointer-events-auto transform-gpu will-change-transform cursor-grab active:cursor-grabbing select-none"
          >
            <!-- Passador Metálico (Clip) — Ponto de conexão do cordão -->
            <div class="badge-clip flex flex-col items-center -mt-4 relative z-10">
              <div class="w-6 md:w-8 h-6 md:h-8 rounded-full border-[3px] border-zinc-400 dark:border-zinc-500 bg-[var(--color-bg-surface)] shadow-[0_2px_8px_rgba(0,0,0,0.2)]"></div>
            </div>

            <!-- Corpo do Crachá -->
            <div class="p-3 md:p-4 flex flex-col gap-3 md:gap-4">
              <!-- Câmera / Notch -->
              <div class="w-full flex justify-center items-center border-b border-[var(--color-border)] pb-2 md:pb-3">
                <div class="w-10 md:w-12 h-2.5 md:h-3 bg-zinc-800 dark:bg-zinc-800 rounded-full relative shadow-inner">
                  <div class="absolute inset-x-3 top-0 h-1 bg-zinc-700 rounded-full"></div>
                </div>
              </div>

              <!-- Foto com Blob Morph -->
              <div class="relative w-full aspect-[3/4] overflow-hidden bg-gradient-to-tr from-[var(--color-ultraviolet)] to-[var(--color-magenta)] p-[2px] animate-blob-morph">
                <div class="w-full h-full bg-[var(--color-bg-main)] animate-blob-morph overflow-hidden">
                  <img src="../assets/hero.png" alt="Hellen Verena" class="w-full h-full object-cover object-top mix-blend-luminosity hover:mix-blend-normal transition-all duration-700 scale-105" draggable="false" />
                </div>
              </div>

              <!-- Código de barras / ID -->
              <div class="border-t border-[var(--color-border)] pt-2 md:pt-3 flex flex-col items-center gap-1 font-mono">
                <span class="text-[9px] md:text-[10px] text-[var(--color-text-muted)] tracking-widest">SST_H_MAGALHAES_2026</span>
                <div class="w-full h-5 md:h-6 bg-[var(--color-text-pure)] opacity-10 rounded-sm mt-1 flex gap-[2px] p-1 overflow-hidden">
                  <div class="h-full bg-current w-1"></div><div class="h-full bg-current w-[2px]"></div><div class="h-full bg-current w-1"></div><div class="h-full bg-current w-[3px]"></div><div class="h-full bg-current w-[1px]"></div><div class="h-full bg-current w-2"></div><div class="h-full bg-current w-[2px]"></div><div class="h-full bg-current w-1"></div><div class="h-full bg-current w-[3px]"></div><div class="h-full bg-current w-1"></div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>

    </div>

    <!-- Barra inferior -->
    <div class="hero-footer opacity-0 w-full flex flex-col sm:flex-row justify-between items-center font-mono text-[10px] md:text-xs text-[var(--color-text-muted)] border-t border-[var(--color-border)] pt-4 md:pt-6 mt-8 md:mt-12 z-10 gap-2">
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
import { ref, onMounted, onUnmounted, nextTick } from 'vue'
import { gsap } from 'gsap'
import { Draggable } from 'gsap/Draggable'

gsap.registerPlugin(Draggable)

// ─── Referências ────────────────────────────────────────────────────────────
const particleCanvas = ref(null)
const badgeRef = ref(null)
const badgeContainer = ref(null)
const cordSvgRef = ref(null)
const cordPathRef = ref(null)

let animationFrameId = null
let draggableInstance = null
let idleTween = null

// ─── Atualizar Cordão SVG (Bezier Quadrática) ──────────────────────────────
function updateCord() {
  const badge = badgeRef.value
  const clip = badge?.querySelector('.badge-clip')
  const svg = cordSvgRef.value
  const path = cordPathRef.value

  if (!badge || !clip || !svg || !path) return

  const svgRect = svg.getBoundingClientRect()
  const clipRect = clip.getBoundingClientRect()
  const containerRect = badgeContainer.value.getBoundingClientRect()

  // Ponto final: centro-topo do passador metálico
  const endX = clipRect.left + clipRect.width / 2 - svgRect.left
  const endY = clipRect.top + clipRect.height / 2 - svgRect.top

  // Ponto âncora: topo-centro do container do crachá, acima do viewport
  const startX = containerRect.left + containerRect.width / 2 - svgRect.left
  const startY = -40

  // Ponto de controle: cria a curvatura natural do cordão
  const dx = endX - startX
  const horizontalDisplacement = Math.abs(dx)
  const sag = 25 + horizontalDisplacement * 0.2

  const ctrlX = (startX + endX) / 2 + dx * 0.08
  const ctrlY = (startY + endY) / 2 + sag

  path.setAttribute('d', `M ${startX},${startY} Q ${ctrlX},${ctrlY} ${endX},${endY}`)
}

// ─── Configurar Draggable ───────────────────────────────────────────────────
function setupDraggable() {
  if (!badgeRef.value) return

  draggableInstance = Draggable.create(badgeRef.value, {
    type: 'x,y',
    edgeResistance: 0.5,
    onPress() {
      // Matar animação idle durante o drag
      if (idleTween) idleTween.kill()
      // Cursor visual
      gsap.set(badgeRef.value, { cursor: 'grabbing' })
    },
    onDrag() {
      updateCord()
    },
    onDragEnd() {
      gsap.set(badgeRef.value, { cursor: 'grab' })
      // Spring back — física de pêndulo/mola
      gsap.to(badgeRef.value, {
        x: 0,
        y: 0,
        rotation: 0,
        duration: 2,
        ease: 'elastic.out(1, 0.3)',
        onUpdate: updateCord,
        onComplete: () => {
          if (draggableInstance && draggableInstance[0]) {
            draggableInstance[0].update()
          }
          startIdleSway()
        }
      })
    }
  })
}

// ─── Animação Idle — Balanço suave de pêndulo ───────────────────────────────
function startIdleSway() {
  if (idleTween) idleTween.kill()
  idleTween = gsap.to(badgeRef.value, {
    rotation: 2,
    duration: 3,
    ease: 'sine.inOut',
    yoyo: true,
    repeat: -1,
    onUpdate: updateCord
  })
}

// ─── Canvas de Partículas ───────────────────────────────────────────────────
function startParticles() {
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
  const quantidade = window.innerWidth < 768 ? 20 : 40

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
}

// ─── Lifecycle ──────────────────────────────────────────────────────────────
onMounted(async () => {
  await nextTick()

  startParticles()

  // Entrada Cinética: Crachá cai de fora da tela
  if (badgeRef.value) {
    gsap.set(badgeRef.value, { y: -window.innerHeight, opacity: 0 })

    // Delay para o crachá cair após o texto começar a aparecer
    gsap.to(badgeRef.value, {
      y: 0,
      opacity: 1,
      duration: 2.5,
      delay: 0.8,
      ease: 'elastic.out(1, 0.3)',
      onUpdate: updateCord,
      onComplete: () => {
        setupDraggable()
        startIdleSway()
      }
    })
  }
})

onUnmounted(() => {
  cancelAnimationFrame(animationFrameId)
  if (idleTween) idleTween.kill()
  if (draggableInstance) {
    draggableInstance.forEach(d => d.kill())
  }
})
</script>