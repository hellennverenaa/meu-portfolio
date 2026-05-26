<script setup>
import {
  Layers, Code, Database, Settings, Cpu, Wrench, GitBranch, Box
} from '@lucide/vue'

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
  <section id="sobre" class="sobre-mim-section relative py-20 md:py-32 lg:py-40 px-4 md:px-12 lg:px-16">
    <div class="max-w-7xl mx-auto">
      <div class="grid grid-cols-1 lg:grid-cols-2 gap-12 md:gap-20 lg:gap-28 items-start">

        <!-- Coluna esquerda: texto + métricas -->
        <div class="flex flex-col gap-8 md:gap-10">
          <span class="sobre-label gs-hidden font-mono text-xs font-medium tracking-[0.2em] uppercase text-[var(--color-magenta)]">
            § Sobre Mim
          </span>
          <h2 class="sobre-title gs-hidden text-3xl sm:text-4xl md:text-5xl lg:text-7xl font-black tracking-brutal leading-[0.9] text-[var(--color-text-pure)]">
            Onde o software
            <span class="block text-transparent bg-clip-text bg-gradient-to-r from-[var(--color-ultraviolet)] to-[var(--color-magenta)] mt-1">encontra a fábrica.</span>
          </h2>
          <div class="flex flex-col gap-4 md:gap-5">
            <p class="sobre-text gs-hidden text-[var(--color-text-muted)] text-base md:text-lg leading-relaxed">
              A minha vivência direta na indústria têxtil ensinou-me que software
              elegante que não responde às restrições do chão de fábrica é inútil.
              Construo ferramentas baseadas na realidade: tempos de ciclo, gestão
              brutal de inventário e redução implacável de desperdícios.
            </p>
            <p class="sobre-text gs-hidden text-[var(--color-text-muted)] text-base md:text-lg leading-relaxed">
              Trago a filosofia <strong class="text-[var(--color-text-pure)] font-semibold">Lean e diagnósticos A3</strong>
              para a arquitetura de código, garantindo queries eficientes e
              processos em lote que rodam de forma silenciosa e perfeita.
            </p>
          </div>

          <!-- Métricas -->
          <div class="grid grid-cols-3 gap-4 md:gap-6 mt-2 md:mt-4">
            <div class="sobre-stat gs-hidden flex flex-col border-l-2 border-[var(--color-magenta)] pl-3 md:pl-4">
              <span class="text-2xl md:text-3xl font-black text-[var(--color-text-pure)]">3+</span>
              <span class="font-mono text-[9px] md:text-[10px] tracking-[0.15em] uppercase text-[var(--color-text-muted)] mt-1">Sistemas Ativos</span>
            </div>
            <div class="sobre-stat gs-hidden flex flex-col border-l-2 border-[var(--color-ultraviolet)] pl-3 md:pl-4">
              <span class="text-2xl md:text-3xl font-black text-[var(--color-text-pure)]">14%</span>
              <span class="font-mono text-[9px] md:text-[10px] tracking-[0.15em] uppercase text-[var(--color-text-muted)] mt-1">Menos Desperdício</span>
            </div>
            <div class="sobre-stat gs-hidden flex flex-col border-l-2 border-[var(--color-ultraviolet)]/50 pl-3 md:pl-4">
              <span class="text-xl md:text-3xl font-black text-[var(--color-text-pure)]">g/100m</span>
              <span class="font-mono text-[9px] md:text-[10px] tracking-[0.15em] uppercase text-[var(--color-text-muted)] mt-1">Conversão Precisa</span>
            </div>
          </div>
        </div>

        <!-- Coluna direita: Foto Estática + Competências -->
        <div class="flex flex-col gap-8 md:gap-10">

          <!-- Foto Estática -->
          <div class="sobre-photo gs-hidden relative w-full max-w-xs md:max-w-sm mx-auto border border-[var(--color-border)] bg-[var(--color-bg-surface)]/30 backdrop-blur-md p-3 md:p-4 rounded-xl shadow-[0_10px_40px_rgba(112,0,255,0.1)] transform-gpu">
            <div class="relative aspect-[3/4] w-full grayscale hover:grayscale-0 transition-all duration-700 overflow-hidden rounded-lg border border-[var(--color-ultraviolet)]/20">
              <img src="../assets/hero.png" alt="Hellen Verena — Retrato Estático" class="w-full h-full object-cover object-top" />
              <div class="absolute bottom-2 left-2 bg-black/80 px-2 py-1 rounded text-[10px] font-mono text-[var(--color-terminal)]">
                VISAO_ESTATICA.PNG
              </div>
            </div>
            <div class="mt-3 md:mt-4 font-mono text-xs text-left space-y-1">
              <p class="text-[var(--color-text-pure)] font-bold">REGISTRO: Magalhães, H. V.</p>
              <p class="text-[var(--color-text-muted)]">NÚCLEO: Core/Bahia/BR</p>
            </div>
            <div class="absolute -inset-px rounded-xl bg-gradient-to-b from-[var(--color-ultraviolet)]/10 to-transparent pointer-events-none -z-10"></div>
          </div>

          <!-- Grid de Competências -->
          <div class="flex flex-col gap-4">
            <span class="font-mono text-xs font-medium tracking-[0.2em] uppercase text-[var(--color-text-muted)]/60">
              Stack & Ferramentas
            </span>
            <div class="grid grid-cols-1 sm:grid-cols-2 gap-2 md:gap-3">
              <div
                v-for="comp in competencias"
                :key="comp.nome"
                class="sobre-comp gs-hidden group flex items-center gap-3 md:gap-4 p-3 md:p-4
                       bg-[var(--color-bg-surface)]/40 backdrop-blur-sm
                       border border-[var(--color-border)] hover:border-[var(--color-ultraviolet)]/40
                       rounded-xl
                       hover:-translate-y-0.5
                       transform-gpu transition-all duration-400 ease-[cubic-bezier(0.32,0.72,0,1)] cursor-default"
              >
                <div class="p-2 md:p-2.5 rounded-lg bg-[var(--color-ultraviolet)]/8 text-[var(--color-ultraviolet)] group-hover:text-[var(--color-magenta)] group-hover:scale-110 transition-all duration-300">
                  <component :is="comp.icone" class="w-4 h-4" />
                </div>
                <span class="font-semibold text-xs md:text-sm text-[var(--color-text-muted)] group-hover:text-[var(--color-text-pure)] transition-colors duration-300">
                  {{ comp.nome }}
                </span>
              </div>
            </div>
          </div>

        </div>

      </div>
    </div>
  </section>
</template>
