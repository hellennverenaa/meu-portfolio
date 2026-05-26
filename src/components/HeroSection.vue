<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import { ArrowRight, Download } from '@lucide/vue'

// ─── Canvas de Partículas Terracotta ─────────────────────────────────────────
const referenciaCanvas = ref(null)
let idAnimacao = null
const cursor = { x: -9999, y: -9999 }

function inicializarCanvas() {
  const tela = referenciaCanvas.value
  if (!tela) return
  const ctx = tela.getContext('2d')

  const TOTAL = 70
  let particulas = []
  let larguraLogica = 0
  let alturaLogica = 0

  function redimensionar() {
    const dpr = window.devicePixelRatio || 1
    larguraLogica = tela.offsetWidth
    alturaLogica = tela.offsetHeight
    tela.width = larguraLogica * dpr
    tela.height = alturaLogica * dpr
    ctx.setTransform(dpr, 0, 0, dpr, 0, 0)
  }

  class Particula {
    constructor() { this.reposicionar() }
    reposicionar() {
      this.x = Math.random() * larguraLogica
      this.y = Math.random() * alturaLogica
      this.vx = (Math.random() - 0.5) * 0.25
      this.vy = (Math.random() - 0.5) * 0.25
      this.raio = Math.random() * 1.2 + 0.4
      this.opacidade = Math.random() * 0.3 + 0.08
    }
    atualizar() {
      this.x += this.vx
      this.y += this.vy
      if (this.x < 0) this.x = larguraLogica
      if (this.x > larguraLogica) this.x = 0
      if (this.y < 0) this.y = alturaLogica
      if (this.y > alturaLogica) this.y = 0
    }
    desenhar() {
      ctx.beginPath()
      ctx.arc(this.x, this.y, this.raio, 0, Math.PI * 2)
      ctx.fillStyle = `rgba(201, 100, 66, ${this.opacidade})`
      ctx.fill()
    }
  }

  function desenharConstelacao() {
    const raio = 140
    for (let i = 0; i < particulas.length; i++) {
      const p = particulas[i]
      const dx = cursor.x - p.x
      const dy = cursor.y - p.y
      const dist = Math.sqrt(dx * dx + dy * dy)
      if (dist < raio) {
        const intensidade = 1 - dist / raio
        ctx.beginPath()
        ctx.moveTo(cursor.x, cursor.y)
        ctx.lineTo(p.x, p.y)
        ctx.strokeStyle = `rgba(201, 100, 66, ${intensidade * 0.25})`
        ctx.lineWidth = intensidade * 1.2
        ctx.stroke()
      }
    }
  }

  function renderizar() {
    ctx.clearRect(0, 0, larguraLogica, alturaLogica)
    for (const p of particulas) { p.atualizar(); p.desenhar() }
    desenharConstelacao()
    idAnimacao = requestAnimationFrame(renderizar)
  }

  redimensionar()
  particulas = Array.from({ length: TOTAL }, () => new Particula())
  const aoRedimensionar = () => { redimensionar(); particulas.forEach(p => p.reposicionar()) }
  window.addEventListener('resize', aoRedimensionar)
  renderizar()

  onUnmounted(() => {
    cancelAnimationFrame(idAnimacao)
    window.removeEventListener('resize', aoRedimensionar)
  })
}

function aoMoverCursor(e) {
  const rect = referenciaCanvas.value?.getBoundingClientRect()
  if (!rect) return
  cursor.x = e.clientX - rect.left
  cursor.y = e.clientY - rect.top
}
function aoSairDaTela() { cursor.x = -9999; cursor.y = -9999 }

onMounted(() => inicializarCanvas())

function irPara(id) {
  document.getElementById(id)?.scrollIntoView({ behavior: 'smooth' })
}
</script>

<template>
  <section
    id="inicio"
    class="relative min-h-screen flex items-center overflow-hidden"
    @pointermove="aoMoverCursor"
    @pointerleave="aoSairDaTela"
  >
    <!-- Canvas de partículas -->
    <canvas
      ref="referenciaCanvas"
      class="absolute inset-0 w-full h-full z-0 transform-gpu will-change-transform opacity-60"
    />

    <!-- Glow orgânico difuso -->
    <div
      class="absolute top-1/3 left-1/4 w-[500px] h-[500px] pointer-events-none z-[1]
             bg-[#C96442]/[0.06] blur-[120px] rounded-[40%_60%_65%_35%/45%_35%_65%_55%]"
    />

    <!-- Conteúdo principal -->
    <div class="relative z-10 w-full max-w-7xl mx-auto px-6 md:px-12 lg:px-16 py-32 md:py-40">
      <div class="grid grid-cols-1 lg:grid-cols-12 gap-16 lg:gap-8 items-center">

        <!-- Coluna esquerda: texto -->
        <div class="lg:col-span-7 flex flex-col gap-10">
          <!-- Badge -->
          <div class="hero-badge gs-hidden inline-flex items-center gap-3 self-start
                      px-4 py-2 border border-[#2E2B27] rounded-full">
            <span class="relative flex h-2 w-2">
              <span class="animate-ping absolute inline-flex h-full w-full rounded-full bg-[#C96442] opacity-50"></span>
              <span class="relative inline-flex rounded-full h-2 w-2 bg-[#C96442]"></span>
            </span>
            <span class="font-[family-name:var(--font-mono)] text-[11px] font-medium tracking-[0.15em] uppercase text-[#7A7570]">
              Disponível para projetos
            </span>
          </div>

          <!-- Título editorial -->
          <h1 class="hero-title font-[family-name:var(--font-editorial)] text-[clamp(2.8rem,8vw,6.5rem)] font-bold tracking-[-0.04em] leading-[0.9] text-[#EDE8DF]">
            <span class="gs-hidden inline-block">Engenharia</span>
            <br />
            <span class="gs-hidden inline-block">de Software</span>
            <br />
            <span class="gs-hidden inline-block text-[#C96442]">Industrial.</span>
          </h1>

          <!-- Subtítulo -->
          <p class="hero-sub gs-hidden font-[family-name:var(--font-body)] text-lg md:text-xl text-[#7A7570] max-w-xl leading-relaxed">
            Sistemas de alta performance moldados para o chão de fábrica.
            Redução de desperdício, controle de inventário e otimização
            impiedosa de processos produtivos.
          </p>

          <!-- Botões -->
          <div class="hero-buttons gs-hidden flex flex-wrap items-center gap-5 mt-2">
            <!-- Botão Primário: Projetos -->
            <button
              @click="irPara('projetos')"
              class="group inline-flex items-center gap-3 px-8 py-4
                     bg-[#C96442] text-[#0F0E0C] font-bold text-sm tracking-wide
                     rounded-full
                     shadow-[0_4px_20px_rgba(201,100,66,0.25)]
                     hover:shadow-[0_8px_30px_rgba(201,100,66,0.35)] hover:-translate-y-0.5
                     active:scale-95 active:translate-y-0
                     focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-[#C96442]/50 focus-visible:ring-offset-2 focus-visible:ring-offset-[#0F0E0C]
                     transform-gpu transition-all duration-500 ease-[cubic-bezier(0.25,1,0.5,1)]
                     cursor-pointer"
            >
              Ver Projetos
              <ArrowRight class="w-4 h-4 group-hover:translate-x-1 transition-transform duration-300" />
            </button>

            <!-- Botão Secundário: Baixar CV -->
            <a
              href="/cv.pdf"
              download
              class="group inline-flex items-center gap-3 px-8 py-4
                     border border-[#2E2B27] text-[#7A7570] font-semibold text-sm tracking-wide
                     rounded-full
                     hover:border-[#C96442]/40 hover:text-[#EDE8DF] hover:-translate-y-0.5
                     active:scale-95 active:translate-y-0
                     focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-[#C96442]/50
                     transform-gpu transition-all duration-500 ease-[cubic-bezier(0.25,1,0.5,1)]"
            >
              <Download class="w-4 h-4 group-hover:-translate-y-0.5 group-hover:text-[#C96442] transition-all duration-300" />
              Baixar Currículo
            </a>
          </div>
        </div>

        <!-- Coluna direita: foto de perfil com máscara orgânica -->
        <div class="lg:col-span-5 flex justify-center lg:justify-end">
          <div class="hero-photo gs-hidden relative">
            <!-- Glow atrás da foto -->
            <div class="absolute -inset-8 bg-[#C96442]/[0.08] blur-3xl rounded-[50%_50%_40%_60%/60%_40%_60%_40%]"></div>

            <!-- Container da foto com máscara orgânica -->
            <div class="relative w-64 h-72 md:w-80 md:h-[22rem] overflow-hidden
                        rounded-[60%_40%_55%_45%/50%_60%_40%_50%]
                        border-2 border-[#2E2B27]
                        bg-[#1C1A17] flex items-center justify-center">
              <!-- Placeholder: Iniciais estilizadas (substituir por <img> quando tiver a foto) -->
              <div class="flex flex-col items-center gap-3">
                <span class="font-[family-name:var(--font-editorial)] text-6xl font-bold text-[#C96442]/30">H</span>
                <span class="font-[family-name:var(--font-mono)] text-[10px] tracking-[0.3em] uppercase text-[#7A7570]/50">
                  foto de perfil
                </span>
              </div>
            </div>
          </div>
        </div>

      </div>
    </div>

    <!-- Indicador de scroll -->
    <div class="absolute bottom-10 left-1/2 -translate-x-1/2 flex flex-col items-center gap-3 z-10">
      <span class="font-[family-name:var(--font-mono)] text-[9px] tracking-[0.3em] uppercase text-[#7A7570]/60">scroll</span>
      <div class="w-px h-12 bg-gradient-to-b from-[#C96442]/40 to-transparent"></div>
    </div>
  </section>
</template>
