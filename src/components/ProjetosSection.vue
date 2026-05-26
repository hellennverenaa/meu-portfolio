<script setup>
import { Database, Scissors, GraduationCap, Settings, Layout } from '@lucide/vue'

const projetos = [
  {
    id: 'scale',
    nome: 'SCALE',
    icone: Database,
    problema:
      'Desvio sistemático no consumo de matéria-prima causado pela ausência de cálculo dinâmico de gramatura exata (g/100m) distribuída por máquina de costura ativa.',
    arquitetura:
      'Construção do front-end reativo em Vue 3 integrado a painéis de acompanhamento e análise detalhada de regras de negócio para o cálculo de gramatura em tempo real. A solução consome uma API em Node.js com banco PostgreSQL e reduziu o desperdício de matéria-prima em 14%.',
    pilha: ['Vue 3', 'Node.js', 'PostgreSQL', 'Regras de Negócio'],
    categoria: 'Projeto Corporativo',
    destaque: true,
  },
  {
    id: 'sic',
    nome: 'SIC (Sistema Informativo de Comunicados)',
    icone: Settings,
    problema:
      'Entrega de alta urgência solicitada pela gestão para mitigar falhas de comunicação e desvio de informações críticas entre unidades produtivas.',
    arquitetura:
      'Sistema automatizado de comunicação no chão de fábrica. Desenvolvi um robô que captura e-mails de modelagem da unidade Sul, processa os dados em um banco centralizado e dispara alertas diretamente para um Dashboard. A interface é acessada pelos operadores bipando o QR Code de cada modelo na linha de produção.',
    pilha: ['JavaScript', 'Google Apps Script', 'Automação', 'QR Code'],
    categoria: 'Projeto em Produção',
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
    categoria: 'Projeto Corporativo',
    destaque: false,
  },
  {
    id: 'almoxarifado',
    nome: 'Portal do Almoxarifado',
    icone: Layout,
    problema:
      'Processo de auditoria física de estoque lento, dependente de papelada física e preenchimento de planilhas manuais suscetíveis a erro humano.',
    arquitetura:
      'Dashboard responsivo e automatizado criado para ser operado via Tablet no centro de distribuição. Permite a realização de auditorias de estoque em tempo real e alimenta um painel central de controle na nuvem de forma automática.',
    pilha: ['JavaScript', 'Google Apps Script', 'UI/UX Mobile', 'Tablet First'],
    categoria: 'Projeto em Produção',
    destaque: false,
  },
  {
    id: 'lunna',
    nome: 'Projeto Lunna',
    icone: GraduationCap,
    problema:
      'Desenvolvimento de um aplicativo de alta performance focado na saúde e bem-estar para controle de rotinas e acompanhamento médico.',
    arquitetura:
      'Desenvolvido inteiramente em React Native no front-end móvel, integrado a uma API REST com isolamento de escopo no back-end. Defendido com nota máxima como Trabalho de Conclusão de Curso.',
    pilha: ['React Native', 'REST API', 'Saúde'],
    categoria: 'Projeto Acadêmico',
    destaque: false,
  },
]
</script>

<template>
  <section id="projetos" class="relative py-20 md:py-32 lg:py-40 px-4 md:px-12 lg:px-16 scroll-mt-20">
    <div class="max-w-7xl mx-auto">

      <!-- Cabeçalho da seção -->
      <div class="mb-12 md:mb-20 lg:mb-28 flex flex-col md:flex-row md:items-end justify-between gap-6 md:gap-8">
        <div class="max-w-2xl">
          <span class="projeto-label gs-hidden font-mono text-xs font-medium tracking-[0.2em] uppercase text-[var(--color-magenta)] block mb-4 md:mb-6">
            § Projetos
          </span>
          <h2 class="projeto-title gs-hidden text-3xl sm:text-4xl md:text-5xl lg:text-7xl font-black tracking-brutal leading-[0.9] text-[var(--color-text-pure)]">
            Sistemas em
            <span class="text-transparent bg-clip-text bg-gradient-to-r from-[var(--color-ultraviolet)] to-[var(--color-magenta)]">Produção.</span>
          </h2>
        </div>
        <p class="projeto-desc gs-hidden text-[var(--color-text-muted)] max-w-sm leading-relaxed font-medium text-sm md:text-base">
          Ferramentas que resolvem gargalos logísticos industriais com métricas mensuráveis de economia.
        </p>
      </div>

      <!-- Grid de Projetos -->
      <div class="grid grid-cols-1 lg:grid-cols-12 gap-4 md:gap-6">
        <article
          v-for="(projeto, index) in projetos"
          :key="projeto.id"
          :class="[
            'projeto-card gs-hidden group relative flex flex-col p-6 md:p-8 lg:p-10',
            projeto.destaque ? 'lg:col-span-7' : 'lg:col-span-5',
            'bg-[var(--color-bg-surface)]/40 backdrop-blur-2xl',
            'border border-[var(--color-border)] hover:border-[var(--color-ultraviolet)]/40',
            'rounded-2xl',
            'hover:-translate-y-1',
            'active:scale-[0.99]',
            'transform-gpu transition-all duration-500 ease-[cubic-bezier(0.25,1,0.5,1)]',
            'hover:shadow-[0_15px_40px_rgba(112,0,255,0.15)]',
          ]"
        >
          <!-- Borda de refração de vidro no topo -->
          <div class="absolute top-0 left-0 right-0 h-px bg-gradient-to-r from-transparent via-[var(--color-ultraviolet)]/30 to-transparent rounded-t-2xl"></div>

          <!-- Glow hover -->
          <div class="absolute inset-0 rounded-2xl bg-gradient-to-b from-[var(--color-ultraviolet)]/5 to-transparent opacity-0 group-hover:opacity-100 transition-opacity duration-500 pointer-events-none"></div>

          <!-- Cabeçalho do card -->
          <div class="flex items-start justify-between mb-6 md:mb-8 relative z-10">
            <div class="flex items-center gap-3">
              <div class="w-10 md:w-12 h-10 md:h-12 flex items-center justify-center rounded-xl
                          bg-[var(--color-ultraviolet)]/10 text-[var(--color-ultraviolet)] border border-[var(--color-ultraviolet)]/15
                          group-hover:text-[var(--color-magenta)] group-hover:border-[var(--color-magenta)]/30
                          group-hover:rotate-6 transition-all duration-500 ease-[cubic-bezier(0.34,1.56,0.64,1)]">
                <component :is="projeto.icone" class="w-4 md:w-5 h-4 md:h-5" />
              </div>
              <span v-if="projeto.categoria" class="px-2.5 py-1 font-mono text-[8px] tracking-wider uppercase bg-[var(--color-magenta)]/10 text-[var(--color-magenta)] rounded border border-[var(--color-magenta)]/25">
                {{ projeto.categoria }}
              </span>
            </div>
            <span class="font-mono text-[10px] tracking-[0.2em] uppercase text-[var(--color-text-muted)]/50 mt-2">
              § {{ String(index + 1).padStart(2, '0') }}
            </span>
          </div>

          <h3 class="relative z-10 text-xl md:text-2xl lg:text-3xl font-bold tracking-tight text-[var(--color-text-pure)] mb-4 md:mb-6">
            {{ projeto.nome }}
          </h3>

          <!-- Conteúdo -->
          <div class="relative z-10 flex flex-col gap-4 md:gap-6 mb-8 md:mb-10 flex-1">
            <div>
              <h4 class="font-mono text-[10px] font-semibold uppercase tracking-[0.2em] text-[var(--color-magenta)] mb-2">
                Problema
              </h4>
              <p class="text-[var(--color-text-muted)] leading-relaxed text-xs md:text-sm">
                {{ projeto.problema }}
              </p>
            </div>
            <div v-if="projeto.destaque">
              <h4 class="font-mono text-[10px] font-semibold uppercase tracking-[0.2em] text-[var(--color-magenta)] mb-2">
                Solução
              </h4>
              <p class="text-[var(--color-text-muted)] leading-relaxed text-xs md:text-sm">
                {{ projeto.arquitetura }}
              </p>
            </div>
          </div>

          <!-- Tags -->
          <div class="relative z-10 flex flex-wrap gap-2 mt-auto pt-4 md:pt-6 border-t border-[var(--color-border)]">
            <span
              v-for="tech in projeto.pilha"
              :key="tech"
              class="px-2.5 md:px-3 py-1 md:py-1.5 font-mono text-[9px] md:text-[10px] font-medium tracking-wider
                     bg-[var(--color-bg-main)]/60 text-[var(--color-text-muted)]
                     border border-[var(--color-border)]
                     rounded-full"
            >
              {{ tech }}
            </span>
          </div>
        </article>
      </div>
    </div>
  </section>
</template>
