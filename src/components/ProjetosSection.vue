<script setup>
import { Database, Scissors, GraduationCap } from '@lucide/vue'

const projetos = [
  {
    id: 'scale',
    nome: 'SCALE',
    icone: Database,
    problema:
      'Desvio sistemático no consumo de matéria-prima causado pela ausência de cálculo dinâmico de gramatura exata (g/100m) distribuída por máquina de costura ativa.',
    arquitetura:
      'Engine de processamento em lote em Node.js com persistência via PostgreSQL e Prisma ORM. O módulo recebe a ordem de produção, calcula o fracionamento de cada insumo por posto de trabalho e reduziu o desperdício em 14%.',
    pilha: ['Node.js', 'PostgreSQL', 'Prisma', 'Vue 3'],
    destaque: true,
  },
  {
    id: 'sobracorte',
    nome: 'SobraCorte',
    icone: Scissors,
    problema:
      'Perda de rastreabilidade nas sobras físicas de lotes de corte e acumulação desordenada de cones de linha vazios no almoxarifado.',
    arquitetura:
      'Módulo web reativo em Vue 3 para processamento em lote de saldos de matéria-prima e gestão em tempo real do inventário de cones e devoluções ao estoque central.',
    pilha: ['Vue 3', 'Tailwind CSS', 'Inventário'],
    destaque: false,
  },
  {
    id: 'lunna',
    nome: 'Projeto Lunna',
    icone: GraduationCap,
    problema:
      'Requisito acadêmico de conceber uma plataforma estável integrando controle de permissões, painéis analíticos e relatórios de produção.',
    arquitetura:
      'Arquitetura full-stack com isolamento de escopo, Node.js no backend e Vue 3 no frontend. Apresentado e defendido com excelência como Trabalho de Conclusão de Curso.',
    pilha: ['Full-stack', 'REST API', 'Escopo Isolado'],
    destaque: false,
  },
]
</script>

<template>
  <section id="projetos" class="relative py-32 md:py-40 px-6 md:px-12 lg:px-16">
    <div class="max-w-7xl mx-auto">

      <!-- Cabeçalho da seção -->
      <div class="mb-20 md:mb-28 flex flex-col md:flex-row md:items-end justify-between gap-8">
        <div class="max-w-2xl">
          <span class="projeto-label gs-hidden font-[family-name:var(--font-mono)] text-xs font-medium tracking-[0.2em] uppercase text-[#C96442] block mb-6">
            § Projetos
          </span>
          <h2 class="projeto-title gs-hidden font-[family-name:var(--font-editorial)] text-5xl md:text-7xl font-bold tracking-[-0.03em] leading-[0.9] text-[#EDE8DF]">
            Sistemas em
            <span class="text-[#C96442]">Produção.</span>
          </h2>
        </div>
        <p class="projeto-desc gs-hidden text-[#7A7570] max-w-sm leading-relaxed font-medium text-base">
          Ferramentas que resolvem gargalos logísticos industriais com métricas mensuráveis de economia.
        </p>
      </div>

      <!-- Grid de Projetos -->
      <div class="grid grid-cols-1 lg:grid-cols-12 gap-6">
        <article
          v-for="(projeto, index) in projetos"
          :key="projeto.id"
          :class="[
            'projeto-card gs-hidden group relative flex flex-col p-8 md:p-10',
            projeto.destaque ? 'lg:col-span-7' : 'lg:col-span-5',
            'bg-[#1C1A17]/60 backdrop-blur-xl',
            'border border-[#2E2B27] hover:border-[#C96442]/30',
            'rounded-2xl',
            'hover:-translate-y-1',
            'active:scale-[0.99]',
            'transform-gpu transition-all duration-500 ease-[cubic-bezier(0.25,1,0.5,1)]',
          ]"
        >
          <!-- Linha de destaque terracotta no topo -->
          <div class="absolute top-0 left-8 right-8 h-px bg-gradient-to-r from-transparent via-[#C96442]/30 to-transparent"></div>

          <!-- Cabeçalho do card -->
          <div class="flex items-start justify-between mb-8">
            <div class="w-12 h-12 flex items-center justify-center rounded-xl
                        bg-[#C96442]/10 text-[#C96442] border border-[#C96442]/15
                        group-hover:rotate-6 transition-transform duration-500 ease-[cubic-bezier(0.34,1.56,0.64,1)]">
              <component :is="projeto.icone" class="w-5 h-5" />
            </div>
            <span class="font-[family-name:var(--font-mono)] text-[10px] tracking-[0.2em] uppercase text-[#7A7570]/50 mt-2">
              § {{ String(index + 1).padStart(2, '0') }}
            </span>
          </div>

          <h3 class="font-[family-name:var(--font-editorial)] text-2xl md:text-3xl font-bold tracking-tight text-[#EDE8DF] mb-6">
            {{ projeto.nome }}
          </h3>

          <!-- Conteúdo -->
          <div class="flex flex-col gap-6 mb-10 flex-1">
            <div>
              <h4 class="font-[family-name:var(--font-mono)] text-[10px] font-semibold uppercase tracking-[0.2em] text-[#C96442] mb-2">
                Problema
              </h4>
              <p class="text-[#7A7570] leading-relaxed text-sm">
                {{ projeto.problema }}
              </p>
            </div>
            <div v-if="projeto.destaque">
              <h4 class="font-[family-name:var(--font-mono)] text-[10px] font-semibold uppercase tracking-[0.2em] text-[#C96442] mb-2">
                Solução
              </h4>
              <p class="text-[#7A7570] leading-relaxed text-sm">
                {{ projeto.arquitetura }}
              </p>
            </div>
          </div>

          <!-- Tags -->
          <div class="flex flex-wrap gap-2 mt-auto pt-6 border-t border-[#2E2B27]">
            <span
              v-for="tech in projeto.pilha"
              :key="tech"
              class="px-3 py-1.5 font-[family-name:var(--font-mono)] text-[10px] font-medium tracking-wider
                     bg-[#2E2B27]/50 text-[#7A7570] rounded-full"
            >
              {{ tech }}
            </span>
          </div>
        </article>
      </div>
    </div>
  </section>
</template>
