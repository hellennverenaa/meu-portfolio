<script setup>
import { Database, Settings, Factory } from '@lucide/vue'

const servicos = [
  {
    id: 'banco-dados',
    titulo: 'Arquitetura de Banco de Dados',
    icone: Database,
    descricao: 'Modelagem relacional avançada, índices compostos e otimização cirúrgica de queries PostgreSQL. Redução de tempo de resposta em consultas complexas com milhões de registros.',
    destaques: ['PostgreSQL', 'Prisma ORM', 'Índices Compostos', 'Query Planner'],
  },
  {
    id: 'otimizacao',
    titulo: 'Otimização de Processos',
    icone: Settings,
    descricao: 'Aplicação de Lean Manufacturing e diagnósticos A3 diretamente na arquitetura de software. Mapeamento de fluxo de valor (VSM) traduzido em lógica de sistemas.',
    destaques: ['Lean', 'Metodologia A3', 'VSM', 'Kaizen'],
  },
  {
    id: 'chao-fabrica',
    titulo: 'Soluções de Chão de Fábrica',
    icone: Factory,
    descricao: 'Sistemas de inventário em tempo real, rastreabilidade de matéria-prima e cálculo de gramatura por máquina ativa. Software que fala a língua da produção.',
    destaques: ['Inventário', 'Rastreabilidade', 'Gramatura g/100m', 'Tempo Real'],
  },
]
</script>

<template>
  <section id="servicos" class="relative py-20 md:py-32 lg:py-40 px-4 md:px-12 lg:px-16 scroll-mt-20">
    <div class="max-w-7xl mx-auto">

      <!-- Cabeçalho da seção -->
      <div class="mb-12 md:mb-20 lg:mb-28 max-w-2xl">
        <span class="servico-label gs-hidden font-mono text-xs font-medium tracking-[0.2em] uppercase text-[var(--color-magenta)] block mb-4 md:mb-6">
          § Serviços
        </span>
        <h2 class="servico-title gs-hidden text-3xl sm:text-4xl md:text-5xl lg:text-7xl font-black tracking-brutal leading-[0.9] text-[var(--color-text-pure)]">
          Engenharia que
          <span class="text-transparent bg-clip-text bg-gradient-to-r from-[var(--color-ultraviolet)] to-[var(--color-magenta)]">resolve.</span>
        </h2>
        <p class="servico-desc gs-hidden mt-6 md:mt-8 text-[var(--color-text-muted)] max-w-lg leading-relaxed text-sm md:text-base">
          Cada solução é construída sob medida para eliminar gargalos reais de operações industriais.
        </p>
      </div>

      <!-- Grid de Cartões Glassmorphism Acheron -->
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4 md:gap-6">
        <article
          v-for="(servico, index) in servicos"
          :key="servico.id"
          class="servico-card gs-hidden group relative flex flex-col p-6 md:p-8 lg:p-10
                 bg-[var(--color-bg-surface)]/40 backdrop-blur-2xl
                 border border-[var(--color-border)]
                 rounded-2xl
                 hover:-translate-y-2
                 active:scale-[0.99]
                 transform-gpu transition-all duration-500 ease-[cubic-bezier(0.25,1,0.5,1)]
                 hover:shadow-[0_8px_40px_rgba(112,0,255,0.2)] hover:border-[var(--color-ultraviolet)]/40"
        >
          <!-- Borda de reflexo no topo -->
          <div class="absolute top-0 left-0 right-0 h-px bg-gradient-to-r from-transparent via-[var(--color-ultraviolet)]/40 to-transparent rounded-t-2xl"></div>

          <!-- Glow sutil de fundo -->
          <div class="absolute inset-0 rounded-2xl bg-gradient-to-b from-[var(--color-ultraviolet)]/5 to-transparent opacity-0 group-hover:opacity-100 transition-opacity duration-500 pointer-events-none"></div>

          <!-- Cabeçalho do card -->
          <div class="flex items-start justify-between mb-6 md:mb-8 relative z-10">
            <div class="w-12 md:w-14 h-12 md:h-14 flex items-center justify-center rounded-xl md:rounded-2xl
                        bg-[var(--color-ultraviolet)]/10 text-[var(--color-ultraviolet)]
                        border border-[var(--color-ultraviolet)]/15
                        group-hover:text-[var(--color-magenta)] group-hover:border-[var(--color-magenta)]/30
                        group-hover:shadow-[0_0_20px_rgba(255,0,127,0.2)]
                        group-hover:rotate-6
                        transition-all duration-500 ease-[cubic-bezier(0.34,1.56,0.64,1)]">
              <component :is="servico.icone" class="w-5 md:w-6 h-5 md:h-6" />
            </div>
            <span class="font-mono text-[10px] tracking-[0.2em] uppercase text-[var(--color-text-muted)]/40 mt-2">
              § {{ String(index + 1).padStart(2, '0') }}
            </span>
          </div>

          <!-- Título -->
          <h3 class="relative z-10 text-lg md:text-xl lg:text-2xl font-bold tracking-tight text-[var(--color-text-pure)] mb-3 md:mb-4">
            {{ servico.titulo }}
          </h3>

          <!-- Descrição -->
          <p class="relative z-10 text-[var(--color-text-muted)] leading-relaxed text-xs md:text-sm mb-6 md:mb-8 flex-1">
            {{ servico.descricao }}
          </p>

          <!-- Tags de destaque -->
          <div class="relative z-10 flex flex-wrap gap-2 mt-auto pt-4 md:pt-6 border-t border-[var(--color-border)]">
            <span
              v-for="tag in servico.destaques"
              :key="tag"
              class="px-2.5 md:px-3 py-1 md:py-1.5 font-mono text-[9px] md:text-[10px] font-medium tracking-wider
                     bg-[var(--color-bg-main)]/60 text-[var(--color-text-muted)]
                     border border-[var(--color-border)]
                     rounded-full
                     group-hover:border-[var(--color-ultraviolet)]/20 group-hover:text-[var(--color-ultraviolet)]
                     transition-all duration-300"
            >
              {{ tag }}
            </span>
          </div>
        </article>
      </div>

    </div>
  </section>
</template>
