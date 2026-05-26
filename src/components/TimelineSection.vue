<script setup>
const experiencias = [
  {
    marcador: '§ 01',
    periodo: 'Dez/2025 — Presente',
    cargo: 'Desenvolvedora Front-End & Automação',
    empresa: 'Grupo Dass',
    descricao:
      'Atuação 100% alocada no desenvolvimento de soluções internas, dashboards e automações para o chão de fábrica. Criação de sistemas de alta urgência utilizando JavaScript (Google Apps Script), integrando fluxos de e-mail, bases de dados e hardware (tablets e leitores de QR Code) para otimizar a operação industrial.',
    pilha: ['JavaScript', 'Google Apps Script', 'Dashboards', 'Automação'],
  },
  {
    marcador: '§ 02',
    periodo: 'Jul/2025 — Jan/2026',
    cargo: 'Estagiária de TI / Automação',
    empresa: 'Grupo Dass',
    descricao:
      'Levantamento de requisitos e modelagem de regras de negócio para transição de controles manuais para sistemas digitais, conectando TI e chão de fábrica.',
    pilha: ['Vue 3', 'Node.js', 'Modelagem', 'Mapeamento'],
  },
  {
    marcador: '§ 03',
    periodo: 'Ago/2023 — Dez/2025',
    cargo: 'Assistente de Consumo / Testes de Produção',
    empresa: 'Grupo Dass',
    descricao:
      'Análise de dados de consumo real vs. previsto e validação de fluxo produtivo de calçados (Nike/Fila). Experiência fundamental para entender as regras de negócio que hoje aplico na criação de softwares.',
    pilha: ['Análise de Dados', 'Excel', 'KPIs', 'Processos'],
  },
]
</script>

<template>
  <section id="carreira" class="relative py-20 md:py-32 lg:py-40 px-4 md:px-12 lg:px-16 scroll-mt-20">
    <div class="max-w-7xl mx-auto">

      <!-- Cabeçalho -->
      <div class="mb-12 md:mb-20 lg:mb-28 max-w-2xl">
        <span class="timeline-label gs-hidden font-mono text-xs font-medium tracking-[0.2em] uppercase text-[var(--color-magenta)] block mb-4 md:mb-6">
          § Carreira
        </span>
        <h2 class="timeline-title gs-hidden text-3xl sm:text-4xl md:text-5xl lg:text-7xl font-black tracking-brutal leading-[0.9] text-[var(--color-text-pure)]">
          Linha do
          <span class="text-transparent bg-clip-text bg-gradient-to-r from-[var(--color-ultraviolet)] to-[var(--color-magenta)]">Tempo.</span>
        </h2>
      </div>

      <!-- Timeline -->
      <div class="timeline relative">
        <!-- Fio vertical brilhante -->
        <div class="timeline-line absolute left-3 md:left-8 top-0 bottom-0 w-px bg-[var(--color-magenta)]/30 origin-top">
          <div class="absolute inset-0 w-px bg-[var(--color-magenta)] shadow-[0_0_8px_rgba(255,0,127,0.6)] origin-top" style="transform: scaleY(0)"></div>
        </div>

        <!-- Items da timeline -->
        <div class="flex flex-col gap-12 md:gap-16 lg:gap-24">
          <div
            v-for="(exp, i) in experiencias"
            :key="i"
            class="timeline-item gs-hidden relative pl-10 md:pl-20"
          >
            <!-- Marcador no fio -->
            <div class="absolute left-0 md:left-4 top-1 w-6 md:w-8 h-6 md:h-8 flex items-center justify-center">
              <div class="w-2.5 md:w-3 h-2.5 md:h-3 rounded-full border-2 border-[var(--color-magenta)] bg-[var(--color-bg-main)] shadow-[0_0_10px_rgba(255,0,127,0.3)]"></div>
            </div>

            <!-- Cabeçalho do item -->
            <div class="flex flex-col sm:flex-row sm:items-baseline gap-1 sm:gap-6 mb-3 md:mb-4">
              <span class="font-mono text-[10px] md:text-xs font-semibold tracking-[0.15em] uppercase text-[var(--color-magenta)]">
                {{ exp.marcador }}
              </span>
              <span class="font-mono text-[10px] md:text-xs tracking-wider text-[var(--color-text-muted)]">
                {{ exp.periodo }}
              </span>
            </div>

            <!-- Cargo e empresa -->
            <h3 class="text-xl md:text-2xl lg:text-3xl font-bold tracking-tight text-[var(--color-text-pure)] mb-1 md:mb-2">
              {{ exp.cargo }}
            </h3>
            <p class="text-xs md:text-sm font-medium text-[var(--color-text-muted)] mb-4 md:mb-5">
              {{ exp.empresa }}
            </p>

            <!-- Descrição -->
            <p class="text-[var(--color-text-muted)] leading-relaxed text-sm md:text-base max-w-2xl mb-4 md:mb-6">
              {{ exp.descricao }}
            </p>

            <!-- Pilha -->
            <div class="flex flex-wrap gap-2">
              <span
                v-for="tech in exp.pilha"
                :key="tech"
                class="px-2.5 md:px-3 py-1 md:py-1.5 font-mono text-[9px] md:text-[10px] font-medium tracking-wider
                       bg-[var(--color-bg-surface)]/50 text-[var(--color-text-muted)]
                       rounded-full border border-[var(--color-border)]"
              >
                {{ tech }}
              </span>
            </div>
          </div>
        </div>
      </div>

    </div>
  </section>
</template>
