<script setup>
import { ref, onMounted, onUnmounted, nextTick } from 'vue'
import {
  Sun,
  Moon,
  Database,
  Scissors,
  GraduationCap,
  ArrowRight,
  ArrowDown,
  Mail,
  GitBranch,
  Layers,
  Wrench,
  Box,
  Cpu,
  Code,
  Settings
} from '@lucide/vue'

// ─── Controle de Tema (Escuro / Claro) ──────────────────────────────────────
const modoEscuro = ref(true)

function alternarTema() {
  modoEscuro.value = !modoEscuro.value
  document.documentElement.classList.toggle('dark', modoEscuro.value)
}

// ─── Referência do Canvas e Posição do Cursor ───────────────────────────────
const referenciaCanvas = ref(null)
let idAnimacao = null
const cursor = { x: -9999, y: -9999 }

// ─── Motor de Partículas — Chuvinha Magnética a 60 FPS ──────────────────────
function inicializarCanvas() {
  const tela = referenciaCanvas.value
  if (!tela) return
  const ctx = tela.getContext('2d')

  const TOTAL = 90
  let particulas = []
  let larguraLogica = 0
  let alturaLogica = 0

  // Ajusta resolução física ao devicePixelRatio para nitidez em telas Retina
  function redimensionar() {
    const dpr = window.devicePixelRatio || 1
    larguraLogica = tela.offsetWidth
    alturaLogica = tela.offsetHeight
    tela.width = larguraLogica * dpr
    tela.height = alturaLogica * dpr
    ctx.setTransform(dpr, 0, 0, dpr, 0, 0)
  }

  class Particula {
    constructor() {
      this.reposicionar()
    }

    reposicionar() {
      this.x = Math.random() * larguraLogica
      this.y = Math.random() * alturaLogica
      this.vx = (Math.random() - 0.5) * 0.35
      this.vy = (Math.random() - 0.5) * 0.35
      this.raio = Math.random() * 1.0 + 1.0
      this.opacidade = Math.random() * 0.35 + 0.1
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
      ctx.fillStyle = `rgba(52, 211, 153, ${this.opacidade})`
      ctx.fill()
    }
  }

  // Linhas de constelação magnética entre cursor e partículas próximas
  function desenharConstelacao() {
    const raio = 150
    for (let i = 0; i < particulas.length; i++) {
      const p = particulas[i]

      // Conexão cursor → partícula
      const dx = cursor.x - p.x
      const dy = cursor.y - p.y
      const dist = Math.sqrt(dx * dx + dy * dy)

      if (dist < raio) {
        const intensidade = 1 - dist / raio
        ctx.beginPath()
        ctx.moveTo(cursor.x, cursor.y)
        ctx.lineTo(p.x, p.y)
        ctx.strokeStyle = `rgba(52, 211, 153, ${intensidade * 0.3})`
        ctx.lineWidth = intensidade * 1.5
        ctx.stroke()
      }

      // Conexões sutis entre partículas vizinhas
      for (let j = i + 1; j < particulas.length; j++) {
        const p2 = particulas[j]
        const dx2 = p.x - p2.x
        const dy2 = p.y - p2.y
        const d2 = Math.sqrt(dx2 * dx2 + dy2 * dy2)

        if (d2 < 90) {
          ctx.beginPath()
          ctx.moveTo(p.x, p.y)
          ctx.lineTo(p2.x, p2.y)
          ctx.strokeStyle = `rgba(52, 211, 153, ${(1 - d2 / 90) * 0.05})`
          ctx.lineWidth = 0.4
          ctx.stroke()
        }
      }
    }
  }

  // Loop de renderização contínuo via requestAnimationFrame
  function renderizar() {
    ctx.clearRect(0, 0, larguraLogica, alturaLogica)
    for (let i = 0; i < particulas.length; i++) {
      particulas[i].atualizar()
      particulas[i].desenhar()
    }
    desenharConstelacao()
    idAnimacao = requestAnimationFrame(renderizar)
  }

  redimensionar()
  particulas = Array.from({ length: TOTAL }, () => new Particula())

  const aoRedimensionar = () => {
    redimensionar()
    particulas.forEach(p => p.reposicionar())
  }
  window.addEventListener('resize', aoRedimensionar)
  renderizar()

  onUnmounted(() => {
    cancelAnimationFrame(idAnimacao)
    window.removeEventListener('resize', aoRedimensionar)
  })
}

// ─── Eventos de Ponteiro ────────────────────────────────────────────────────
function aoMoverCursor(evento) {
  const rect = referenciaCanvas.value?.getBoundingClientRect()
  if (!rect) return
  cursor.x = evento.clientX - rect.left
  cursor.y = evento.clientY - rect.top
}

function aoSairDaTela() {
  cursor.x = -9999
  cursor.y = -9999
}

// ─── Montagem ───────────────────────────────────────────────────────────────
onMounted(() => {
  document.documentElement.classList.add('dark')
  nextTick(() => inicializarCanvas())
})

// ─── Navegação Suave ────────────────────────────────────────────────────────
function irPara(id) {
  document.getElementById(id)?.scrollIntoView({ behavior: 'smooth' })
}

// ─── Dados dos Projetos ─────────────────────────────────────────────────────
const projetos = [
  {
    id: 'scale',
    nome: 'SCALE',
    icone: Database,
    problema:
      'Desvio sistemático no consumo de matéria-prima causado pela ausência de cálculo dinâmico de gramatura exata (g/100m) distribuída por máquina de costura ativa.',
    arquitetura:
      'Engine de processamento em lote em Node.js com persistência via PostgreSQL e Prisma ORM. O módulo recebe a ordem de produção, calcula o fracionamento de cada insumo por posto de trabalho e reduziu o desperdício em 14%.',
    pilha: ['Node.js', 'PostgreSQL', 'Prisma ORM', 'Vue 3'],
    destaque: true,
  },
  {
    id: 'sobracorte',
    nome: 'SobraCorte',
    icone: Scissors,
    problema:
      'Perda de rastreabilidade nas sobras físicas de lotes de corte e acumulação desordenada de cones de linha vazios no almoxarifado, impedindo a reconciliação fiável do inventário.',
    arquitetura:
      'Módulo web reativo em Vue 3 para processamento em lote de saldos de matéria-prima e gestão em tempo real do inventário de cones e devoluções ao estoque central.',
    pilha: ['Vue 3', 'Tailwind CSS', 'Gestão de Inventário'],
    destaque: false,
  },
  {
    id: 'lunna',
    nome: 'Projeto Lunna',
    icone: GraduationCap,
    problema:
      'Requisito acadêmico de conceber uma plataforma estável integrando controle de permissões, painéis analíticos e relatórios de produção numa única base de código.',
    arquitetura:
      'Arquitetura full-stack ponta a ponta com isolamento de escopo, Node.js no backend e Vue 3 no frontend. Apresentado e defendido com excelência como Trabalho de Conclusão de Curso.',
    pilha: ['Full-stack', 'REST API', 'Isolamento de Escopo'],
    destaque: false,
  },
]

// ─── Competências Técnicas ──────────────────────────────────────────────────
const competencias = [
  { nome: 'Vue 3 / Composition API', icone: Layers },
  { nome: 'Node.js', icone: Code },
  { nome: 'PostgreSQL', icone: Database },
  { nome: 'Prisma ORM', icone: Settings },
  { nome: 'Tailwind CSS v4', icone: Cpu },
  { nome: 'Lean / Metodologia A3', icone: Wrench },
  { nome: 'Git & Versionamento', icone: GitBranch },
  { nome: 'Gestão de Inventário', icone: Box },
]
</script>

<template>
  <div class="min-h-screen bg-zinc-950 text-zinc-100 antialiased transition-colors duration-500 dark:bg-zinc-950 dark:text-zinc-100">

    <!-- ═══════════════════════════════════════════ CABEÇALHO FIXO ═══ -->
    <header
      class="fixed top-0 inset-x-0 z-50 flex items-center justify-between
             px-8 md:px-16 py-6
             bg-zinc-950/80 backdrop-blur-2xl
             border-b border-white/5
             transition-colors duration-500"
    >
      <a href="#" @click.prevent="irPara('inicio')" class="text-lg font-bold tracking-tight cursor-pointer">
        <span class="text-transparent bg-clip-text bg-gradient-to-r from-emerald-300 to-cyan-400">hellen</span><span class="text-zinc-500">.dev</span>
      </a>

      <nav class="hidden md:flex items-center gap-10 text-[13px] font-medium text-zinc-500">
        <a href="#projetos" @click.prevent="irPara('projetos')" class="hover:text-zinc-100 transition-colors duration-300">Projetos</a>
        <a href="#sobre" @click.prevent="irPara('sobre')" class="hover:text-zinc-100 transition-colors duration-300">Sobre</a>
        <a href="#contato" @click.prevent="irPara('contato')" class="hover:text-zinc-100 transition-colors duration-300">Contato</a>
      </nav>

      <!-- Alternador de tema com os 5 estados obrigatórios -->
      <button
        @click="alternarTema"
        aria-label="Alternar tema claro e escuro"
        class="p-2 rounded-full
               bg-zinc-900 border border-white/10
               text-zinc-400
               hover:text-amber-300 hover:border-white/20
               active:scale-90
               focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-emerald-400
               disabled:opacity-40
               transform-gpu transition-all duration-300 ease-[cubic-bezier(0.32,0.72,0,1)]
               cursor-pointer"
      >
        <Sun v-if="modoEscuro" class="w-4 h-4" />
        <Moon v-else class="w-4 h-4" />
      </button>
    </header>

    <!-- ═════════════════════════════ SEÇÃO HERO — TIPOGRAFIA DE ALTA COSTURA ═══ -->
    <section
      id="inicio"
      class="relative min-h-screen flex items-center justify-center overflow-hidden"
      @pointermove="aoMoverCursor"
      @pointerleave="aoSairDaTela"
    >
      <!-- Canvas de partículas (absolute inset-0 z-0, acelerado via GPU) -->
      <canvas
        ref="referenciaCanvas"
        class="absolute inset-0 w-full h-full z-0 transform-gpu will-change-transform"
      />

      <!-- Aura radial esmeralda difusa -->
      <div
        class="absolute inset-0 pointer-events-none z-[1]"
        style="background: radial-gradient(ellipse 50% 40% at 50% 45%, rgba(52, 211, 153, 0.06) 0%, transparent 70%)"
      />

      <!-- Conteúdo principal sobre o canvas (z-10) -->
      <div class="relative z-10 flex flex-col items-center text-center px-8 max-w-5xl mx-auto gap-8">

        <!-- Badge de disponibilidade -->
        <div class="inline-flex items-center gap-2 px-4 py-2 rounded-full
                    bg-emerald-500/10 border border-emerald-500/15
                    text-emerald-400 text-[11px] font-semibold tracking-widest uppercase">
          <span class="relative flex h-2 w-2">
            <span class="animate-ping absolute inline-flex h-full w-full rounded-full bg-emerald-400 opacity-60"></span>
            <span class="relative inline-flex rounded-full h-2 w-2 bg-emerald-400"></span>
          </span>
          Disponível para projetos
        </div>

        <!-- Título editorial massivo com degradê esmeralda -->
        <h1 class="text-7xl md:text-9xl font-extrabold tracking-tighter leading-[0.9]">
          <span class="text-transparent bg-clip-text bg-gradient-to-r from-emerald-300 via-teal-300 to-cyan-400">
            Engenharia
          </span>
          <br />
          <span class="text-zinc-100">
            de Software.
          </span>
        </h1>

        <!-- Subtítulo técnico -->
        <p class="text-base md:text-lg text-zinc-500 max-w-xl leading-relaxed">
          Sistemas de alta performance para o chão de fábrica.
          Otimização de queries Prisma, processamento em lote
          e rastreabilidade de inventário industrial.
        </p>

        <!-- Botões com 5 estados (default, hover, active, focus-visible, disabled) -->
        <div class="flex flex-wrap items-center justify-center gap-4 mt-4">
          <button
            @click="irPara('projetos')"
            class="group inline-flex items-center gap-2 px-8 py-4 rounded-2xl
                   font-semibold text-sm text-zinc-950
                   bg-gradient-to-r from-emerald-400 to-cyan-400
                   shadow-[0_8px_30px_rgb(52,211,153,0.2)]
                   hover:shadow-[0_8px_40px_rgb(52,211,153,0.35)] hover:scale-[1.03]
                   active:scale-95
                   focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-emerald-400
                   disabled:opacity-40 disabled:cursor-not-allowed
                   transform-gpu will-change-transform
                   transition-all duration-500 ease-[cubic-bezier(0.32,0.72,0,1)]
                   cursor-pointer"
          >
            Ver projetos
            <ArrowRight class="w-4 h-4 group-hover:translate-x-1 transition-transform duration-300" />
          </button>

          <button
            @click="irPara('contato')"
            class="px-8 py-4 rounded-2xl font-semibold text-sm
                   border border-white/10 text-zinc-400
                   hover:text-zinc-100 hover:border-white/25
                   active:scale-95
                   focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-emerald-400
                   disabled:opacity-40
                   transform-gpu transition-all duration-500 ease-[cubic-bezier(0.32,0.72,0,1)]
                   cursor-pointer"
          >
            Contato
          </button>
        </div>

        <!-- Indicador de rolagem -->
        <button
          @click="irPara('projetos')"
          class="mt-16 flex flex-col items-center gap-2 text-zinc-600
                 hover:text-zinc-400 active:scale-90
                 focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-emerald-400
                 transform-gpu transition-all duration-300 cursor-pointer"
          aria-label="Rolar para projetos"
        >
          <span class="text-[10px] uppercase tracking-[0.3em] font-medium">scroll</span>
          <ArrowDown class="w-4 h-4 animate-bounce" />
        </button>
      </div>
    </section>

    <!-- ═══════════════════════ PROJETOS — LIQUID-GLASS REFRACTION ═══ -->
    <section
      id="projetos"
      class="relative py-32 px-8 md:px-16 overflow-hidden"
    >
      <!-- Gradiente de fundo sutil para profundidade -->
      <div class="absolute inset-0 z-0" style="background: linear-gradient(180deg, rgba(9,9,11,1) 0%, rgba(24,24,27,0.6) 50%, rgba(9,9,11,1) 100%)" />

      <div class="relative z-10 max-w-6xl mx-auto">

        <!-- Cabeçalho da seção, alinhado à esquerda -->
        <div class="mb-16 max-w-xl text-left">
          <p class="text-[11px] font-semibold tracking-[0.2em] uppercase text-emerald-400/80 mb-4">Projetos</p>
          <h2 class="text-4xl md:text-6xl font-extrabold tracking-tighter text-zinc-100">
            Sistemas em<br />Produção.
          </h2>
          <p class="mt-6 text-zinc-500 leading-relaxed">
            Ferramentas construídas para resolver gargalos reais
            de logística interna, cálculo de insumos e rastreabilidade
            de descarte de materiais no chão de fábrica.
          </p>
        </div>

        <!-- Bento Grid assimétrico — SCALE ocupa 2 colunas -->
        <div class="grid grid-cols-1 md:grid-cols-2 gap-8">
          <article
            v-for="projeto in projetos"
            :key="projeto.id"
            :class="[
              projeto.destaque ? 'md:col-span-2' : '',
              'group relative flex flex-col gap-8 p-8 md:p-10 rounded-3xl',
              // ── Liquid-Glass Refraction (elite-ui-ux.md §4) ──
              'bg-slate-900/30 backdrop-blur-2xl',
              'border-t border-white/20 border-l border-white/10 border-r border-white/[0.03] border-b border-white/[0.02]',
              'shadow-[0_8px_30px_rgb(0,0,0,0.12)]',
              // ── Hover com glow interno e levitação ──
              'hover:-translate-y-2 hover:shadow-[0_20px_60px_rgb(0,0,0,0.3),inset_0_1px_0_rgb(255,255,255,0.1)]',
              'hover:border-t-white/30',
              // ── 5 Estados obrigatórios ──
              'active:scale-[0.98]',
              'focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-emerald-400',
              // ── Aceleração GPU + Física de mola ──
              'transform-gpu will-change-transform',
              'transition-all duration-500 ease-[cubic-bezier(0.32,0.72,0,1)]',
              'cursor-default',
            ]"
            tabindex="0"
          >
            <!-- Ícone do projeto -->
            <div class="w-12 h-12 flex items-center justify-center rounded-2xl
                        bg-emerald-500/10 text-emerald-400 border border-emerald-500/15">
              <component :is="projeto.icone" class="w-5 h-5" />
            </div>

            <!-- Título -->
            <h3 class="text-2xl md:text-3xl font-bold tracking-tight text-zinc-100">
              {{ projeto.nome }}
            </h3>

            <!-- Problema de Negócio & Solução de Arquitetura -->
            <div :class="['grid gap-8', projeto.destaque ? 'md:grid-cols-2' : 'grid-cols-1']">
              <div class="text-left">
                <h4 class="text-[10px] font-bold uppercase tracking-[0.2em] text-zinc-600 mb-3">
                  Problema de Negócio
                </h4>
                <p class="text-sm text-zinc-400 leading-relaxed">
                  {{ projeto.problema }}
                </p>
              </div>
              <div class="text-left">
                <h4 class="text-[10px] font-bold uppercase tracking-[0.2em] text-zinc-600 mb-3">
                  Solução de Arquitetura
                </h4>
                <p class="text-sm text-zinc-400 leading-relaxed">
                  {{ projeto.arquitetura }}
                </p>
              </div>
            </div>

            <!-- Tags da pilha tecnológica -->
            <div class="flex flex-wrap gap-2 mt-auto pt-4 border-t border-white/5">
              <span
                v-for="tech in projeto.pilha"
                :key="tech"
                class="px-3 py-1.5 text-[11px] font-medium rounded-lg
                       bg-white/5 text-zinc-400 border border-white/5"
              >
                {{ tech }}
              </span>
            </div>
          </article>
        </div>
      </div>
    </section>

    <!-- ═══════════════════════════════ SOBRE & COMPETÊNCIAS ═══════ -->
    <section id="sobre" class="py-32 px-8 md:px-16">
      <div class="max-w-6xl mx-auto">
        <div class="grid grid-cols-1 lg:grid-cols-2 gap-16 items-start">

          <!-- Coluna esquerda: perfil técnico -->
          <div class="flex flex-col gap-8 text-left">
            <p class="text-[11px] font-semibold tracking-[0.2em] uppercase text-emerald-400/80">Sobre</p>
            <h2 class="text-3xl md:text-5xl font-extrabold tracking-tighter leading-[1.1] text-zinc-100">
              Onde o
              <span class="text-transparent bg-clip-text bg-gradient-to-r from-emerald-300 to-cyan-400">software</span>
              encontra o chão de fábrica.
            </h2>
            <p class="text-zinc-500 leading-relaxed">
              Estudante de
              <strong class="text-zinc-200">Sistemas de Informação</strong>
              com vivência direta na indústria têxtil. Esta experiência permite
              o desenvolvimento de ferramentas que respondem a restrições
              operacionais concretas, com entendimento profundo de tempos,
              métodos e gestão de inventário.
            </p>
            <p class="text-zinc-500 leading-relaxed">
              Aplicação de conceitos
              <strong class="text-zinc-200">Lean e diagnósticos A3</strong>
              para redução de perdas físicas, otimização de queries Prisma e
              processamento em lote de dados de produção em ambientes de alta
              exigência.
            </p>

            <!-- Métricas operacionais — Grid de 8px -->
            <div class="grid grid-cols-3 gap-4 mt-4">
              <div class="p-6 rounded-2xl bg-slate-900/30 backdrop-blur-2xl border-t border-white/10 border border-white/5">
                <div class="text-2xl font-extrabold text-transparent bg-clip-text bg-gradient-to-r from-emerald-300 to-cyan-400">3+</div>
                <div class="text-[10px] uppercase tracking-wider text-zinc-600 mt-2">Sistemas ativos</div>
              </div>
              <div class="p-6 rounded-2xl bg-slate-900/30 backdrop-blur-2xl border-t border-white/10 border border-white/5">
                <div class="text-2xl font-extrabold text-transparent bg-clip-text bg-gradient-to-r from-emerald-300 to-cyan-400">14%</div>
                <div class="text-[10px] uppercase tracking-wider text-zinc-600 mt-2">Menos desperdício</div>
              </div>
              <div class="p-6 rounded-2xl bg-slate-900/30 backdrop-blur-2xl border-t border-white/10 border border-white/5">
                <div class="text-2xl font-extrabold text-transparent bg-clip-text bg-gradient-to-r from-emerald-300 to-cyan-400">g/100m</div>
                <div class="text-[10px] uppercase tracking-wider text-zinc-600 mt-2">Conversão ativa</div>
              </div>
            </div>
          </div>

          <!-- Coluna direita: competências técnicas -->
          <div class="flex flex-col gap-8 text-left">
            <p class="text-[11px] font-semibold tracking-[0.2em] uppercase text-zinc-600">Stack & Ferramentas</p>

            <div class="grid grid-cols-1 sm:grid-cols-2 gap-3">
              <div
                v-for="comp in competencias"
                :key="comp.nome"
                class="group flex items-center gap-3 px-4 py-4 rounded-2xl
                       bg-slate-900/30 backdrop-blur-xl
                       border-t border-white/10 border border-white/5
                       hover:border-emerald-400/30 hover:-translate-y-0.5
                       active:scale-[0.98]
                       focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-emerald-400
                       transform-gpu transition-all duration-300 ease-[cubic-bezier(0.32,0.72,0,1)]
                       cursor-default"
                tabindex="0"
              >
                <div class="p-2 rounded-xl bg-emerald-500/10 text-emerald-400">
                  <component :is="comp.icone" class="w-4 h-4" />
                </div>
                <span class="text-sm font-medium text-zinc-300 group-hover:text-emerald-400 transition-colors duration-300">
                  {{ comp.nome }}
                </span>
              </div>
            </div>

            <!-- Citação técnica -->
            <blockquote class="mt-4 pl-6 border-l-2 border-emerald-500/30 text-zinc-600 text-sm italic leading-relaxed">
              "A eficiência do software no contexto industrial se mede pelo
              tempo de resposta da query e pela facilidade com que o operador
              de máquina insere e valida dados no inventário."
            </blockquote>
          </div>
        </div>
      </div>
    </section>

    <!-- ═══════════════════════════════ CONTATO ════════════════════ -->
    <section id="contato" class="relative py-32 px-8 md:px-16 overflow-hidden">
      <!-- Gradiente de fundo -->
      <div class="absolute inset-0 z-0" style="background: linear-gradient(180deg, rgba(9,9,11,1) 0%, rgba(24,24,27,0.4) 50%, rgba(9,9,11,1) 100%)" />

      <div class="relative z-10 max-w-2xl mx-auto text-center flex flex-col items-center gap-8">
        <p class="text-[11px] font-semibold tracking-[0.2em] uppercase text-emerald-400/80">Contato</p>
        <h2 class="text-3xl md:text-5xl font-extrabold tracking-tighter text-zinc-100">
          Pronta para colaborar.
        </h2>
        <p class="text-zinc-500 leading-relaxed max-w-md">
          Aberta a oportunidades de desenvolvimento voltadas para
          integração industrial, APIs resilientes e otimização de
          infraestruturas com PostgreSQL e Prisma.
        </p>

        <a
          href="mailto:hellen@example.com"
          class="group inline-flex items-center gap-3 px-8 py-4 rounded-2xl
                 font-semibold text-sm text-zinc-950
                 bg-gradient-to-r from-emerald-400 to-cyan-400
                 shadow-[0_8px_30px_rgb(52,211,153,0.2)]
                 hover:shadow-[0_8px_40px_rgb(52,211,153,0.35)] hover:scale-[1.03]
                 active:scale-95
                 focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-emerald-400
                 disabled:opacity-40
                 transform-gpu transition-all duration-500 ease-[cubic-bezier(0.32,0.72,0,1)]"
        >
          <Mail class="w-4 h-4" />
          Iniciar conversa
        </a>
      </div>
    </section>

    <!-- ═══════════════════════════════ RODAPÉ ═════════════════════ -->
    <footer class="py-10 px-8 md:px-16 border-t border-white/5">
      <div class="max-w-6xl mx-auto flex flex-col sm:flex-row items-center justify-between gap-6">
        <p class="text-[13px] text-zinc-600">
          &copy; 2025
          <span class="text-emerald-400 font-medium">hellen.dev</span>
          &mdash; Vue 3, Tailwind CSS v4 e Lucide Icons.
        </p>

        <div class="flex items-center gap-8">
          <a
            href="https://github.com/"
            target="_blank"
            rel="noopener noreferrer"
            aria-label="Perfil no GitHub"
            class="flex items-center gap-2 text-[13px] text-zinc-600
                   hover:text-zinc-100 transition-colors duration-300"
          >
            <svg class="w-4 h-4" fill="currentColor" viewBox="0 0 24 24">
              <path fill-rule="evenodd" clip-rule="evenodd" d="M12 2C6.477 2 2 6.477 2 12c0 4.418 2.865 8.166 6.839 9.489.5.092.682-.217.682-.482 0-.237-.008-.866-.013-1.7-2.782.604-3.369-1.34-3.369-1.34-.454-1.154-1.11-1.462-1.11-1.462-.908-.62.069-.608.069-.608 1.003.07 1.531 1.03 1.531 1.03.892 1.529 2.341 1.087 2.91.832.092-.647.35-1.088.636-1.338-2.22-.253-4.555-1.11-4.555-4.943 0-1.091.39-1.984 1.029-2.683-.103-.253-.446-1.27.098-2.647 0 0 .84-.269 2.75 1.025A9.578 9.578 0 0112 6.836c.85.004 1.705.114 2.504.336 1.909-1.294 2.747-1.025 2.747-1.025.546 1.377.203 2.394.1 2.647.64.699 1.028 1.592 1.028 2.683 0 3.842-2.339 4.687-4.566 4.935.359.309.678.919.678 1.852 0 1.336-.012 2.415-.012 2.743 0 .267.18.578.688.48C19.138 20.163 22 16.418 22 12c0-5.523-4.477-10-10-10z"/>
            </svg>
            GitHub
          </a>
          <a
            href="https://linkedin.com/in/"
            target="_blank"
            rel="noopener noreferrer"
            aria-label="Perfil no LinkedIn"
            class="flex items-center gap-2 text-[13px] text-zinc-600
                   hover:text-zinc-100 transition-colors duration-300"
          >
            <svg class="w-4 h-4" fill="currentColor" viewBox="0 0 24 24">
              <path d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433a2.062 2.062 0 01-2.063-2.065 2.064 2.064 0 112.063 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"/>
            </svg>
            LinkedIn
          </a>
        </div>
      </div>
    </footer>

  </div>
</template>

<style>
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800;900&display=swap');

html {
  scroll-behavior: smooth;
}

body {
  margin: 0;
  padding: 0;
  font-family: 'Inter', system-ui, -apple-system, sans-serif;
  background-color: #09090b;
}
</style>
