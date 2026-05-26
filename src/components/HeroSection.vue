<template>
  <section id="inicio" class="hero-section relative min-h-screen flex flex-col justify-between pt-6 md:pt-6 pb-6 md:pb-4 px-2 md:px-6 max-w-7xl mx-auto z-10 overflow-visible">
    <canvas ref="particleCanvas" class="absolute inset-0 pointer-events-none z-0"></canvas>

    <svg ref="cordSvgRef" class="absolute inset-0 w-full h-full pointer-events-none z-0 overflow-visible">
      <defs>
        <linearGradient id="lanyardGradient" x1="0%" y1="0%" x2="100%" y2="100%">
          <stop offset="0%" stop-color="#7000FF" />
          <stop offset="100%" stop-color="#FF007F" />
        </linearGradient>
      </defs>
      <path ref="lanyardPath" fill="none" stroke="url(#lanyardGradient)" stroke-width="14" stroke-linecap="round" />
    </svg>

    <div class="grid grid-cols-1 lg:grid-cols-12 gap-8 md:gap-12 items-center z-10 w-full my-auto">

      <div class="lg:col-span-7 flex flex-col text-left order-2 lg:order-1">
        <div class="hero-badge opacity-0 inline-flex items-center gap-2 px-3 py-1 rounded-full border border-[var(--color-ultraviolet)]/30 bg-[var(--color-bg-surface)]/50 text-xs font-mono text-[var(--color-magenta)] mb-4 md:mb-6 w-fit backdrop-blur-md">
          <span class="w-2 h-2 rounded-full bg-[var(--color-terminal)] animate-pulse"></span>
          ARQUITETURA DE SOFTWARE & SOLUÇÕES INDUSTRIAIS
        </div>

        <div class="text-[var(--color-magenta)] font-mono text-xs uppercase tracking-[0.2em] mb-2">
          Portfólio Profissional — 2026
        </div>

        <h1 class="hero-title text-4xl sm:text-5xl md:text-6xl lg:text-8xl font-black text-[var(--color-text-pure)] leading-none tracking-brutal uppercase select-none overflow-hidden">
          <span class="gs-hidden block opacity-0 transform translate-y-full">HELLEN</span>
          <span class="gs-hidden block opacity-0 transform translate-y-full text-transparent bg-clip-text bg-gradient-to-r from-[var(--color-ultraviolet)] to-[var(--color-magenta)]">VERENA</span>
        </h1>

        <p class="hero-sub opacity-0 mt-6 md:mt-8 text-base md:text-lg lg:text-xl text-[var(--color-text-muted)] max-w-xl font-normal leading-relaxed">
          Especialista em otimização extrema de <span class="text-[var(--color-text-pure)] font-mono">PostgreSQL</span> e arquitetura com <span class="text-[var(--color-text-pure)] font-mono">Prisma ORM</span>. Desenvolvendo sistemas inteligentes de alta performance para o chão de fábrica industrial.
        </p>

        <div class="hero-buttons opacity-0 mt-8 md:mt-10 flex flex-wrap gap-3 md:gap-4">
          <a href="#sobre" class="group relative px-6 md:px-8 py-3 md:py-4 bg-[var(--color-ultraviolet)] hover:bg-[var(--color-magenta)] text-white font-medium rounded-full transition-all duration-500 ease-[cubic-bezier(0.32,0.72,0,1)] transform-gpu hover:scale-105 shadow-[0_0_25px_rgba(112,0,255,0.4)] hover:shadow-[0_0_30px_rgba(255,0,127,0.6)] active:scale-95 focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-[var(--color-magenta)]/50 text-sm md:text-base">
            Saber Mais
          </a>
          <a href="#contato" class="px-6 md:px-8 py-3 md:py-4 rounded-full border border-[var(--color-border)] hover:border-[var(--color-magenta)] bg-[var(--color-bg-surface)]/40 text-[var(--color-text-pure)] font-medium transition-all duration-300 backdrop-blur-md active:scale-95 focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-[var(--color-ultraviolet)]/50 text-sm md:text-base">
            Iniciar Conexão
          </a>
        </div>
      </div>

      <div class="lg:col-span-5 flex justify-center lg:justify-end relative min-h-[320px] md:min-h-[480px] w-full order-1 lg:order-2">
        <div ref="badgeContainer" class="badge-container relative w-56 md:w-72 lg:w-80 flex items-start justify-center pt-8 md:pt-0">
          <div
            ref="badgeRef"
            class="hero-photo floating-card relative w-48 md:w-64 lg:w-72 bg-[var(--color-bg-surface)]/80 border border-[var(--color-ultraviolet)]/40 rounded-2xl shadow-[0_0_50px_rgba(112,0,255,0.15)] backdrop-blur-xl flex flex-col transition-shadow duration-300 pointer-events-auto transform-gpu will-change-transform cursor-grab active:cursor-grabbing select-none"
            style="opacity: 1; visibility: visible;"
          >
            <div class="badge-clip flex flex-col items-center -mt-4 relative z-10">
              <div class="w-6 md:w-8 h-6 md:h-8 rounded-full border-[3px] border-zinc-400 bg-[var(--color-bg-surface)] shadow-[0_2px_8px_rgba(0,0,0,0.2)]"></div>
            </div>

            <div class="p-3 md:p-4 flex flex-col gap-3 md:gap-4">
              <div class="w-full flex justify-center items-center border-b border-[var(--color-border)] pb-2 md:pb-3">
                <div class="w-10 md:w-12 h-2.5 md:h-3 bg-zinc-800 rounded-full relative shadow-inner">
                  <div class="absolute inset-x-3 top-0 h-1 bg-zinc-700 rounded-full"></div>
                </div>
              </div>

              <div class="relative w-full aspect-[3/4] overflow-hidden bg-gradient-to-tr from-[var(--color-ultraviolet)] to-[var(--color-magenta)] p-[2px] animate-blob-morph">
                <div class="w-full h-full bg-[var(--color-bg-main)] animate-blob-morph overflow-hidden">
                  <img src="../assets/hero.png" alt="Hellen Verena" class="w-full h-full object-cover object-top mix-blend-luminosity hover:mix-blend-normal transition-all duration-700 scale-105" draggable="false" />
                </div>
              </div>

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

    <div class="hero-footer opacity-0 w-full flex flex-col sm:flex-row justify-between items-center font-mono text-[10px] md:text-xs text-[var(--color-text-muted)] border-t border-[var(--color-border)] pt-4 md:pt-6 mt-8 md:mt-12 z-10 gap-4">
      
      <div class="flex items-center gap-4">
        <div class="flex items-center gap-2 text-white">
          <span class="w-2 h-2 bg-[#39FF14] rounded-full animate-pulse shadow-[0_0_10px_#39FF14]"></span>
          SOBRACORTE // ONLINE
        </div>
        <div class="px-3 py-1 rounded-full border border-[#7000FF]/50 bg-[#7000FF]/10 text-[#B282FF] text-[10px] uppercase tracking-widest flex items-center gap-2">
          <span class="w-1.5 h-1.5 bg-[#B282FF] rounded-full"></span>
          Disponível para 2026
        </div>
      </div>

      <div class="flex items-center gap-6">
        <span class="text-[var(--color-text-pure)]">{{ horaAtual }}</span>
        <button @click="rolarPagina" class="animate-bounce text-[var(--color-magenta)] hover:text-[var(--color-text-pure)] transition-colors cursor-pointer">
          ↓ ROLAR PARA EXPLORAR
        </button>
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
const lanyardPath = ref(null)

const horaAtual = ref('')
const atualizarHora = () => {
  const agora = new Date()
  horaAtual.value = agora.toLocaleTimeString('pt-BR', { hour: '2-digit', minute: '2-digit' })
}

let animationFrameId = null
let draggableInstance = null
let idleTween = null

// ─── Função de Scroll Suave Nativa ──────────────────────────────────────────
const rolarPagina = () => {
  window.scrollBy({ top: window.innerHeight, behavior: 'smooth' })
}

// ─── Desenhar Cordão (Bezier Quadrática) ────────────────────────────────────
function drawLanyard() {
  const badge = badgeRef.value
  const clip = badge?.querySelector('.badge-clip')
  const svg = cordSvgRef.value
  const path = lanyardPath.value

  if (!badge || !clip || !svg || !path) return

  const svgRect = svg.getBoundingClientRect()
  const clipRect = clip.getBoundingClientRect()

  // A MÁGICA ESTÁ AQUI:
  // O '0' representa o topo da tela física do usuário (Viewport). 
  // Subtraindo o svgRect.top (que fica negativo no scroll), nós transformamos
  // a coordenada em um valor positivo que anula o movimento da página, 
  // cravando a ponta do cordão eternamente no topo do monitor!
  const startX = (window.innerWidth * 0.78) - svgRect.left
  const startY = 0 - svgRect.top - 50 // Preso 50px acima do limite da tela

  const endX = clipRect.left + clipRect.width / 2 - svgRect.left
  const endY = clipRect.top - svgRect.top

  // Curvatura com física simulada
  const dx = endX - startX
  const sag = 25 + Math.abs(dx) * 0.2
  const ctrlX = (startX + endX) / 2
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
      if (idleTween) idleTween.kill()
      gsap.set(badgeRef.value, { cursor: 'grabbing' })
    },
    onDrag() {
      drawLanyard()
    },
    onDragEnd() {
      gsap.set(badgeRef.value, { cursor: 'grab' })
      gsap.to(badgeRef.value, {
        x: 0,
        y: 0,
        rotation: 0,
        duration: 2,
        ease: 'elastic.out(1, 0.3)',
        onUpdate: drawLanyard,
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

// ─── Animação Idle — Balanço suave ──────────────────────────────────────────
function startIdleSway() {
  if (idleTween) idleTween.kill()
  idleTween = gsap.to(badgeRef.value, {
    rotation: 2,
    duration: 3,
    ease: 'sine.inOut',
    yoyo: true,
    repeat: -1,
    onUpdate: drawLanyard
  })
}

// ─── Canvas de Partículas ───────────────────────────────────────────────────
function startParticles() {
  const canvas = particleCanvas.value
  if (!canvas) return
  const ctx = canvas.getContext('2d')

  const redimensionar = () => {
    if (canvas && canvas.parentElement) {
      canvas.width = canvas.parentElement.offsetWidth
      canvas.height = canvas.parentElement.offsetHeight
    }
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
    if (!canvas || !ctx) return
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

  atualizarHora()
const intervaloHora = setInterval(atualizarHora, 60000)

  await nextTick()

  startParticles()

  // Garante que o cordão acompanhe as transições de scroll do App.vue
  window.addEventListener('scroll', drawLanyard)
  window.addEventListener('resize', drawLanyard)

  // Entrada Cinética do crachá caindo
  if (badgeRef.value) {
    gsap.set(badgeRef.value, { y: -window.innerHeight })

    gsap.to(badgeRef.value, {
      y: 0,
      duration: 2.5,
      delay: 0.8,
      ease: 'elastic.out(1, 0.3)',
      onUpdate: drawLanyard,
      onComplete: () => {
        setupDraggable()
        startIdleSway()
      }
    })
  }
})

onUnmounted(() => {
  cancelAnimationFrame(animationFrameId)
  window.removeEventListener('scroll', drawLanyard)
  window.removeEventListener('resize', drawLanyard)
  clearInterval(intervaloHora)

  if (idleTween) idleTween.kill()
  if (draggableInstance) {
    if (Array.isArray(draggableInstance)) {
      draggableInstance.forEach(d => d.kill())
    } else if (typeof draggableInstance.kill === 'function') {
      draggableInstance.kill()
    }
  }
})
</script>