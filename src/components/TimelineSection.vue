<script setup>
const experiencias = [
  {
    marcador: '§ 01',
    periodo: '2023 — Presente',
    cargo: 'Engenheira de Software',
    empresa: 'Indústria Têxtil — Sistemas Internos',
    descricao:
      'Desenvolvimento e manutenção de sistemas internos para gestão de inventário, cálculo de gramatura por máquina ativa e rastreabilidade de matéria-prima. Responsável pelo módulo SCALE (redução de 14% em desperdício) e SobraCorte (reconciliação de inventário em tempo real).',
    pilha: ['Vue 3', 'Node.js', 'PostgreSQL', 'Prisma'],
  },
  {
    marcador: '§ 02',
    periodo: '2022 — 2023',
    cargo: 'Desenvolvimento Full-Stack — TCC',
    empresa: 'Projeto Lunna — Trabalho de Conclusão de Curso',
    descricao:
      'Concepção e arquitetura de uma plataforma full-stack completa integrando controle de permissões, painéis analíticos e relatórios de produção. Apresentado e defendido com excelência acadêmica.',
    pilha: ['Full-stack', 'REST API', 'Isolamento de Escopo'],
  },
  {
    marcador: '§ 03',
    periodo: '2020 — 2022',
    cargo: 'Estudante de Sistemas de Informação',
    empresa: 'Formação Acadêmica',
    descricao:
      'Fundamentos sólidos em algoritmos, estruturas de dados, banco de dados relacionais e metodologias ágeis. Primeiro contato com Lean Manufacturing e diagnósticos A3 aplicados ao contexto fabril.',
    pilha: ['SQL', 'Algoritmos', 'Lean', 'Metodologia A3'],
  },
]
</script>

<template>
  <section id="carreira" class="relative py-32 md:py-40 px-6 md:px-12 lg:px-16">
    <div class="max-w-7xl mx-auto">

      <!-- Cabeçalho -->
      <div class="mb-20 md:mb-28 max-w-2xl">
        <span class="timeline-label gs-hidden font-[family-name:var(--font-mono)] text-xs font-medium tracking-[0.2em] uppercase text-[#C96442] block mb-6">
          § Carreira
        </span>
        <h2 class="timeline-title gs-hidden font-[family-name:var(--font-editorial)] text-5xl md:text-7xl font-bold tracking-[-0.03em] leading-[0.9] text-[#EDE8DF]">
          Linha do
          <span class="text-[#C96442]">Tempo.</span>
        </h2>
      </div>

      <!-- Timeline -->
      <div class="timeline relative">
        <!-- Fio vertical — cresce com o scroll via GSAP -->
        <div class="timeline-line absolute left-4 md:left-8 top-0 bottom-0 w-px bg-[#2E2B27] origin-top"></div>

        <!-- Items da timeline -->
        <div class="flex flex-col gap-16 md:gap-24">
          <div
            v-for="(exp, i) in experiencias"
            :key="i"
            class="timeline-item gs-hidden relative pl-12 md:pl-20"
          >
            <!-- Marcador no fio -->
            <div class="absolute left-0 md:left-4 top-1 w-8 h-8 flex items-center justify-center">
              <div class="w-3 h-3 rounded-full border-2 border-[#C96442] bg-[#0F0E0C]"></div>
            </div>

            <!-- Cabeçalho do item -->
            <div class="flex flex-col sm:flex-row sm:items-baseline gap-2 sm:gap-6 mb-4">
              <span class="font-[family-name:var(--font-mono)] text-xs font-semibold tracking-[0.15em] uppercase text-[#C96442]">
                {{ exp.marcador }}
              </span>
              <span class="font-[family-name:var(--font-mono)] text-xs tracking-wider text-[#7A7570]">
                {{ exp.periodo }}
              </span>
            </div>

            <!-- Cargo e empresa -->
            <h3 class="font-[family-name:var(--font-editorial)] text-2xl md:text-3xl font-bold tracking-tight text-[#EDE8DF] mb-2">
              {{ exp.cargo }}
            </h3>
            <p class="font-[family-name:var(--font-body)] text-sm font-medium text-[#7A7570] mb-5">
              {{ exp.empresa }}
            </p>

            <!-- Descrição -->
            <p class="text-[#7A7570] leading-relaxed text-base max-w-2xl mb-6">
              {{ exp.descricao }}
            </p>

            <!-- Pilha -->
            <div class="flex flex-wrap gap-2">
              <span
                v-for="tech in exp.pilha"
                :key="tech"
                class="px-3 py-1.5 font-[family-name:var(--font-mono)] text-[10px] font-medium tracking-wider
                       bg-[#2E2B27]/50 text-[#7A7570] rounded-full border border-[#2E2B27]"
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
