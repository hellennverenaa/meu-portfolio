<template>
  <section id="inicio" class="hero-section relative min-h-[100dvh] h-auto flex flex-col justify-between pt-28 md:pt-6 pb-6 md:pb-4 px-2 md:px-6 max-w-7xl mx-auto z-10 overflow-visible">
    <canvas ref="particleCanvas" class="absolute inset-0 pointer-events-none z-0"></canvas>

    <!-- ─── Wrapper de Fade para o ScrollTrigger ─────────────────────────────
         Este div (.hero-fade-wrapper) começa com opacity:1 e NUNCA é tocado
         pelo tlHero (que anima os filhos individualmente). Assim, quando a
         tlPin do App.vue faz scrub neste wrapper, o estado inicial gravado
         é opacity:1 — e ao rolar para cima, o scrub restaura corretamente.
    ────────────────────────────────────────────────────────────────────────── -->
    <div class="hero-fade-wrapper flex flex-col flex-1 justify-between">

      <svg ref="cordSvgRef" class="absolute inset-0 w-full h-full pointer-events-none z-0 overflow-visible">
        <defs>
          <linearGradient id="lanyardGradient" x1="0%" y1="0%" x2="100%" y2="100%">
            <stop offset="0%" stop-color="#7000FF" />
            <stop offset="100%" stop-color="#FF007F" />
          </linearGradient>
        </defs>
        <path ref="lanyardPath" fill="none" stroke="url(#lanyardGradient)" stroke-width="14" stroke-linecap="round" />
      </svg>

      <div class="grid grid-cols-1 lg:grid-cols-12 gap-4 md:gap-15 items-center z-10 w-full pt-0 md:pt-20 pb-10 md:pb-20 relative">

        <div class="lg:col-span-7 flex flex-col text-left order-1 pt-28 md:pt-0 pb-8 md:pb-32 relative z-20">

          <!-- Badge de Arquitetura -->
          <div class="hero-badge opacity-0 hidden md:inline-flex items-center gap-4 px-3 py-1 rounded-full border border-[var(--color-ultraviolet)]/30 bg-[var(--color-bg-surface)]/50 text-xs font-mono text-[var(--color-magenta)] mt-4 md:mt-0 mb-6 md:mb-6 w-fit backdrop-blur-md">
            <span class="w-2 h-2 rounded-full bg-[var(--color-terminal)] animate-pulse"></span>
            ARQUITETURA DE SOFTWARE & SOLUÇÕES INDUSTRIAIS
          </div>

          <div class="text-[var(--color-magenta)] font-mono text-xs uppercase tracking-[0.2em] mb-4 md:mb-2 hidden md:block">
            Portfólio Profissional — 2026
          </div>

          <!-- Badge de Disponibilidade — alta visibilidade, logo abaixo do label -->
          <div class="hero-avail-badge opacity-0 hidden md:inline-flex items-center gap-2.5 px-5 py-2 rounded-full w-fit mb-8 md:mb-6
                      border border-[#7000FF] bg-[#7000FF]/10
                      shadow-[0_0_20px_rgba(112,0,255,0.15),inset_0_0_12px_rgba(112,0,255,0.08)]
                      backdrop-blur-md z-20">
            <span class="relative flex h-2.5 w-2.5">
              <span class="animate-ping absolute inline-flex h-full w-full rounded-full bg-[#39FF14] opacity-75"></span>
              <span class="relative inline-flex rounded-full h-2.5 w-2.5 bg-[#39FF14] shadow-[0_0_8px_#39FF14]"></span>
            </span>
            <span class="font-mono text-[10px] md:text-[11px] uppercase tracking-[0.15em] text-[#7000FF] dark:text-[#B282FF] font-bold">
              DISPONÍVEL — ACEITANDO PROJETOS EM 2026
            </span>
          </div>

          <!-- Cabeçalho Minimalista Mobile -->
          <div class="hero-mobile-header flex flex-col gap-2 md:hidden mb-4 z-20 relative">
            <div class="flex items-center gap-2">
              <span class="w-2 h-2 rounded-full bg-[#00FF00] shadow-[0_0_8px_#00FF00] animate-pulse"></span>
              <span class="text-[10px] font-mono tracking-widest text-neutral-300 uppercase">Aceitando Projetos 2026</span>
            </div>
            <span class="text-[10px] font-mono tracking-widest text-[#FF007F] uppercase">Arquitetura de Software & Soluções Industriais</span>
          </div>

          <h1 class="hero-title text-4xl sm:text-5xl md:text-6xl lg:text-8xl font-black text-[var(--color-text-pure)] leading-none tracking-brutal uppercase select-none overflow-hidden">
            <span class="gs-hidden block opacity-0 transform translate-y-full">HELLEN</span>
            <span class="gs-hidden block opacity-0 transform translate-y-full text-transparent bg-clip-text bg-gradient-to-r from-[var(--color-ultraviolet)] to-[var(--color-magenta)]">VERENA</span>
          </h1>

          <p class="hero-sub opacity-0 mt-8 md:mt-8 text-base md:text-lg lg:text-xl text-[var(--color-text-muted)] max-w-xl font-normal leading-relaxed hidden md:block">
            Especialista em otimização extrema de <span class="text-[var(--color-text-pure)] font-mono">PostgreSQL</span> e arquitetura com <span class="text-[var(--color-text-pure)] font-mono">Prisma ORM</span>. Desenvolvendo sistemas inteligentes de alta performance para o chão de fábrica industrial.
          </p>

          <!-- Desktop Buttons (hidden on mobile) -->
          <div class="hero-buttons opacity-0 mt-10 md:mt-10 hidden md:flex flex-wrap gap-3 md:gap-4">
            <a href="#sobre" class="group relative px-6 md:px-8 py-3 md:py-4 bg-[var(--color-ultraviolet)] hover:bg-[var(--color-magenta)] text-white font-medium rounded-full transition-all duration-500 ease-[cubic-bezier(0.32,0.72,0,1)] transform-gpu hover:scale-105 shadow-[0_0_25px_rgba(112,0,255,0.4)] hover:shadow-[0_0_30px_rgba(255,0,127,0.6)] active:scale-95 focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-[var(--color-magenta)]/50 text-sm md:text-base">
              Saber Mais
            </a>
            <a href="#contato" class="px-6 md:px-8 py-3 md:py-4 rounded-full border border-[var(--color-border)] hover:border-[var(--color-magenta)] bg-[var(--color-bg-surface)]/40 text-[var(--color-text-pure)] font-medium transition-all duration-300 backdrop-blur-md active:scale-95 focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-[var(--color-ultraviolet)]/50 text-sm md:text-base">
              Iniciar Conexão
            </a>
            <a href="/Curriculo-Hellen-Verena-(Desenvolvedora).pdf" target="_blank" download class="px-6 md:px-8 py-3 md:py-4 rounded-full border border-dashed border-[#7000FF] hover:bg-[#7000FF]/20 text-neutral-900 dark:text-white font-medium transition-all duration-300 backdrop-blur-md active:scale-95 focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-[#7000FF]/50 text-sm md:text-base">
              Baixar Currículo
            </a>
          </div>
        </div>

        <div class="absolute md:relative inset-x-0 top-[60%] -translate-y-1/2 md:top-auto md:translate-y-0 z-0 md:z-10 lg:col-span-5 flex justify-center lg:justify-end min-h-[220px] md:min-h-[480px] w-full order-2 pointer-events-none md:pointer-events-auto opacity-50 md:opacity-100">
          <div ref="cardRef" class="badge-container relative w-40 md:w-72 lg:w-80 flex items-start justify-center pt-12 md:pt-0">
            <div
              ref="badgeRef"
              class="hero-photo floating-card relative w-36 md:w-64 lg:w-72 bg-[var(--color-bg-surface)]/80 border border-[var(--color-ultraviolet)]/40 rounded-2xl shadow-[0_0_50px_rgba(112,0,255,0.15)] backdrop-blur-xl flex flex-col transition-shadow duration-300 pointer-events-auto transform-gpu will-change-transform cursor-grab active:cursor-grabbing select-none"
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
                  <span class="text-[9px] md:text-[10px] text-[var(--color-text-muted)] tracking-widest">HELLEN VERENA DA C. MAGALHÃES</span>
                  <div class="w-full h-5 md:h-6 bg-[var(--color-text-pure)] opacity-10 rounded-sm mt-1 flex gap-[2px] p-1 overflow-hidden">
                    <div class="h-full bg-current w-1"></div><div class="h-full bg-current w-[2px]"></div><div class="h-full bg-current w-1"></div><div class="h-full bg-current w-[3px]"></div><div class="h-full bg-current w-[1px]"></div><div class="h-full bg-current w-2"></div><div class="h-full bg-current w-[2px]"></div><div class="h-full bg-current w-1"></div><div class="h-full bg-current w-[3px]"></div><div class="h-full bg-current w-1"></div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>

      </div>

      <!-- Mobile Paragraph & Buttons (hidden on desktop) — Localizados fora do grid, perto do rodapé com cores vivas e opacidade 100% -->
      <div class="md:hidden flex flex-col items-center gap-4 w-full z-20 relative mt-auto px-4 pb-2">
        <p class="hero-sub opacity-0 text-sm text-[var(--color-text-muted)] text-center max-w-sm font-normal leading-relaxed">
          Especialista em otimização extrema de <span class="text-[var(--color-text-pure)] font-mono font-semibold">PostgreSQL</span> e arquitetura com <span class="text-[var(--color-text-pure)] font-mono font-semibold">Prisma ORM</span>. Desenvolvendo sistemas inteligentes de alta performance para o chão de fábrica industrial.
        </p>

        <div class="hero-buttons opacity-0 w-full flex justify-center flex-wrap gap-3 pointer-events-auto">
          <a href="#sobre" class="group relative px-5 py-2.5 bg-[var(--color-ultraviolet)] hover:bg-[var(--color-magenta)] text-white font-semibold rounded-full transition-all duration-500 active:scale-95 text-xs shadow-[0_0_15px_rgba(112,0,255,0.5)]">
            Saber Mais
          </a>
          <a href="#contato" class="px-5 py-2.5 rounded-full border-2 border-[var(--color-ultraviolet)] bg-[var(--color-bg-surface)]/95 text-neutral-900 dark:text-white font-semibold transition-all duration-300 active:scale-95 text-xs">
            Iniciar Conexão
          </a>
          <a href="/Curriculo-Hellen-Verena-(Desenvolvedora).pdf" target="_blank" download class="px-5 py-2.5 rounded-full border-2 border-dashed border-[#FF007F] bg-[var(--color-bg-surface)]/95 text-neutral-900 dark:text-white font-semibold transition-all duration-300 active:scale-95 text-xs">
            Baixar Currículo
          </a>
        </div>
      </div>

      <!-- ─── Rodapé da Hero ───────────────────────────────────────────────── -->
      <div class="hero-footer opacity-0 w-full flex justify-center sm:justify-between items-center font-mono text-[10px] md:text-xs text-[var(--color-text-muted)] border-t border-[var(--color-border)] pt-4 md:pt-6 z-10 gap-4 mt-auto bottom-center">
        
        <!-- Lado Esquerdo (Desktop apenas) -->
        <div class="hidden sm:flex items-center gap-4">
          <div class="flex items-center gap-2 text-neutral-900 dark:text-white">
            <span class="w-2 h-2 bg-[#39FF14] rounded-full animate-pulse shadow-[0_0_10px_#39FF14]"></span>
            SOBRACORTE // ONLINE
          </div>
        </div>

        <!-- Botão Mobile (Centralizado com seta minimalista e pulso) -->
        <div class="flex sm:hidden flex-col items-center justify-center w-full gap-2">
          <div class="animate-pulse">
            <svg class="w-4 h-4 text-[var(--color-magenta)]" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2.5">
              <path stroke-linecap="round" stroke-linejoin="round" d="M19 13l-7 7-7-7m14-6l-7 7-7-7" />
            </svg>
          </div>
          <button @click="rolarPagina" class="cursor-pointer focus-visible:outline-none">
            <span class="font-mono uppercase text-[10px] tracking-widest text-neutral-400">Rolar para explorar</span>
          </button>
        </div>

        <!-- Lado Direito (Desktop apenas) -->
        <div class="hidden sm:flex items-center gap-6">
          <span class="text-neutral-900 dark:text-white">{{ horaAtual }}</span>
          <button @click="rolarPagina" class="animate-bounce text-[var(--color-magenta)] hover:text-[var(--color-text-pure)] transition-colors cursor-pointer">
            ↓ ROLAR PARA EXPLORAR
          </button>
        </div>
      </div>

    </div><!-- fim .hero-fade-wrapper -->
  </section>
</template>

<script setup>
import { ref, onMounted, onUnmounted, nextTick } from 'vue'
import { gsap } from 'gsap'
import { Draggable } from 'gsap/Draggable'
import { ScrollToPlugin } from 'gsap/ScrollToPlugin'

gsap.registerPlugin(Draggable, ScrollToPlugin)

// ─── Referências ────────────────────────────────────────────────────────────
const particleCanvas = ref(null)
const badgeRef = ref(null)
const cardRef = ref(null)
const cordSvgRef = ref(null)
const lanyardPath = ref(null)

// ─── Relógio & Scroll Suave (GSAP) ──────────────────────────────────────────
const horaAtual = ref('')
const atualizarHora = () => {
  const agora = new Date()
  horaAtual.value = agora.toLocaleTimeString('pt-BR', { hour: '2-digit', minute: '2-digit' })
}
let intervaloHora = null

const rolarPagina = () => {
  gsap.to(window, { scrollTo: { y: '#sobre', offsetY: 0 }, duration: 1 })
}

let animationFrameId = null
let draggableInstance = null
let idleTween = null

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
  const startX = (window.innerWidth < 768 ? (window.innerWidth * 0.5) - svgRect.left : (window.innerWidth * 0.78) - svgRect.left)
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
  intervaloHora = setInterval(atualizarHora, 60000)

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

  // Animação de Balanço (Sway Effect) do container do crachá
  if (cardRef.value) {
    gsap.to(cardRef.value, {
      rotation: 6,
      transformOrigin: 'top center',
      repeat: -1,
      yoyo: true,
      duration: 4,
      ease: 'sine.inOut',
      onUpdate: drawLanyard
    })
  }

  // Animação de entrada do cabeçalho minimalista no mobile
  gsap.from('.hero-mobile-header', {
    opacity: 0,
    y: 15,
    duration: 0.8,
    delay: 0.5,
    ease: 'power3.out'
  })
})

onUnmounted(() => {
  clearInterval(intervaloHora)
  cancelAnimationFrame(animationFrameId)
  window.removeEventListener('scroll', drawLanyard)
  window.removeEventListener('resize', drawLanyard)

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