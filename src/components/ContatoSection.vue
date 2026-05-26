<script setup>
import { Mail } from '@lucide/vue'
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
  <!-- ═══════════ SOBRE ═══════════ -->
  <section id="sobre" class="relative py-32 md:py-40 px-6 md:px-12 lg:px-16">
    <div class="max-w-7xl mx-auto">
      <div class="grid grid-cols-1 lg:grid-cols-2 gap-20 lg:gap-28 items-start">

        <!-- Coluna esquerda: texto -->
        <div class="flex flex-col gap-10">
          <span class="sobre-label gs-hidden font-[family-name:var(--font-mono)] text-xs font-medium tracking-[0.2em] uppercase text-[#C96442]">
            § Sobre
          </span>
          <h2 class="sobre-title gs-hidden font-[family-name:var(--font-editorial)] text-5xl md:text-7xl font-bold tracking-[-0.03em] leading-[0.9] text-[#EDE8DF]">
            Onde o software
            <span class="block text-[#C96442] mt-1">encontra a fábrica.</span>
          </h2>
          <div class="flex flex-col gap-5">
            <p class="sobre-text gs-hidden text-[#7A7570] text-lg leading-relaxed">
              A minha vivência direta na indústria têxtil ensinou-me que software
              elegante que não responde às restrições do chão de fábrica é inútil.
              Construo ferramentas baseadas na realidade: tempos de ciclo, gestão
              brutal de inventário e redução implacável de desperdícios.
            </p>
            <p class="sobre-text gs-hidden text-[#7A7570] text-lg leading-relaxed">
              Trago a filosofia <strong class="text-[#EDE8DF] font-semibold">Lean e diagnósticos A3</strong>
              para a arquitetura de código, garantindo queries eficientes e
              processos em lote que rodam de forma silenciosa e perfeita.
            </p>
          </div>

          <!-- Métricas -->
          <div class="grid grid-cols-3 gap-6 mt-4">
            <div class="sobre-stat gs-hidden flex flex-col border-l-2 border-[#C96442] pl-4">
              <span class="font-[family-name:var(--font-editorial)] text-3xl font-bold text-[#EDE8DF]">3+</span>
              <span class="font-[family-name:var(--font-mono)] text-[10px] tracking-[0.15em] uppercase text-[#7A7570] mt-1">Sistemas Ativos</span>
            </div>
            <div class="sobre-stat gs-hidden flex flex-col border-l-2 border-[#C96442]/60 pl-4">
              <span class="font-[family-name:var(--font-editorial)] text-3xl font-bold text-[#EDE8DF]">14%</span>
              <span class="font-[family-name:var(--font-mono)] text-[10px] tracking-[0.15em] uppercase text-[#7A7570] mt-1">Menos Desperdício</span>
            </div>
            <div class="sobre-stat gs-hidden flex flex-col border-l-2 border-[#C96442]/30 pl-4">
              <span class="font-[family-name:var(--font-editorial)] text-3xl font-bold text-[#EDE8DF]">g/100m</span>
              <span class="font-[family-name:var(--font-mono)] text-[10px] tracking-[0.15em] uppercase text-[#7A7570] mt-1">Conversão Precisa</span>
            </div>
          </div>
        </div>

        <!-- Coluna direita: competências -->
        <div class="flex flex-col gap-8">
          <span class="font-[family-name:var(--font-mono)] text-xs font-medium tracking-[0.2em] uppercase text-[#7A7570]/60">
            Stack & Ferramentas
          </span>
          <div class="grid grid-cols-1 sm:grid-cols-2 gap-3">
            <div
              v-for="comp in competencias"
              :key="comp.nome"
              class="sobre-comp gs-hidden group flex items-center gap-4 p-4
                     bg-[#1C1A17]/60 backdrop-blur-sm
                     border border-[#2E2B27] hover:border-[#C96442]/30
                     rounded-xl
                     hover:-translate-y-0.5
                     transform-gpu transition-all duration-400 ease-out cursor-default"
            >
              <div class="p-2.5 rounded-lg bg-[#C96442]/8 text-[#C96442] group-hover:scale-110 transition-transform duration-300">
                <component :is="comp.icone" class="w-4 h-4" />
              </div>
              <span class="font-semibold text-sm text-[#7A7570] group-hover:text-[#EDE8DF] transition-colors duration-300">
                {{ comp.nome }}
              </span>
            </div>
          </div>
        </div>

      </div>
    </div>
  </section>

  <!-- ═══════════ CONTATO ═══════════ -->
  <section id="contato" class="relative py-32 md:py-40 px-6 md:px-12 lg:px-16 text-center">
    <div class="max-w-3xl mx-auto flex flex-col items-center gap-10">
      <span class="contato-label gs-hidden font-[family-name:var(--font-mono)] text-xs font-medium tracking-[0.2em] uppercase text-[#C96442]">
        § Contato
      </span>
      <h2 class="contato-title gs-hidden font-[family-name:var(--font-editorial)] text-5xl md:text-8xl font-bold tracking-[-0.03em] leading-[0.9] text-[#EDE8DF]">
        Vamos construir
        <span class="block text-[#C96442] mt-2">o futuro.</span>
      </h2>

      <p class="contato-text gs-hidden text-xl text-[#7A7570] max-w-xl leading-relaxed">
        Aberta a oportunidades focadas em resolver problemas industriais
        complexos com código elegante e escalável.
      </p>

      <a
        href="mailto:hellen@example.com"
        class="contato-cta gs-hidden group mt-4 inline-flex items-center gap-4 px-10 py-5
               bg-[#C96442] text-[#0F0E0C]
               font-bold text-base tracking-wide
               rounded-full
               shadow-[0_4px_20px_rgba(201,100,66,0.25)]
               hover:shadow-[0_8px_30px_rgba(201,100,66,0.35)] hover:-translate-y-1
               active:scale-95 active:translate-y-0
               transform-gpu transition-all duration-500 ease-[cubic-bezier(0.25,1,0.5,1)]"
      >
        <Mail class="w-5 h-5 group-hover:-rotate-12 transition-transform duration-300" />
        Iniciar Conversa
      </a>
    </div>
  </section>

  <!-- ═══════════ RODAPÉ ═══════════ -->
  <footer class="py-12 px-6 md:px-12 lg:px-16 border-t border-[#2E2B27]">
    <div class="max-w-7xl mx-auto flex flex-col md:flex-row items-center justify-between gap-6">
      <p class="font-[family-name:var(--font-mono)] text-xs text-[#7A7570] tracking-wider">
        &copy; 2025 <strong class="text-[#EDE8DF]">hellen.dev</strong>
      </p>
      <div class="flex gap-8">
        <a href="https://github.com/" target="_blank" rel="noopener noreferrer"
           class="font-[family-name:var(--font-mono)] text-xs tracking-widest uppercase text-[#7A7570] hover:text-[#C96442] transition-colors duration-300">
          GitHub
        </a>
        <a href="https://linkedin.com/in/" target="_blank" rel="noopener noreferrer"
           class="font-[family-name:var(--font-mono)] text-xs tracking-widest uppercase text-[#7A7570] hover:text-[#C96442] transition-colors duration-300">
          LinkedIn
        </a>
      </div>
    </div>
  </footer>
</template>
