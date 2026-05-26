<script setup>
// Competências movidas para o MarqueeBand
</script>

<template>
  <section id="sobre" class="sobre-mim-section relative py-20 md:py-32 lg:py-40 px-4 md:px-12 lg:px-16 scroll-mt-20">
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
              Minha trajetória profissional é fundamentada na vivência industrial real, atuando diretamente em cargos como <strong class="text-[var(--color-text-pure)] font-semibold">Assistente de Consumo</strong> e <strong class="text-[var(--color-text-pure)] font-semibold">Auxiliar de Custos</strong>. Essa experiência prática me deu uma compreensão profunda sobre como identificar e eliminar gargalos de produção no chão de fábrica.
            </p>
            <p class="sobre-text gs-hidden text-[var(--color-text-muted)] text-base md:text-lg leading-relaxed">
              Essa base operacional e analítica fundamenta diretamente a forma como construo soluções robustas utilizando <strong class="text-[var(--color-text-pure)] font-semibold">Node.js e PostgreSQL</strong>. Desenvolvo sistemas focados na reconciliação precisa de estoque, controle rigoroso de resíduos industriais e rastreamento de desperdícios, conectando regras de negócio complexas à realidade física da produção.
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

          <!-- Foto Estática com animação de flutuação -->
          <div class="sobre-photo gs-hidden relative w-full max-w-xs md:max-w-sm mx-auto border border-[var(--color-border)] bg-[var(--color-bg-surface)]/30 backdrop-blur-md p-3 md:p-4 rounded-xl shadow-[0_10px_40px_rgba(112,0,255,0.1)] transform-gpu animate-float">
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

          <!-- Bloco Corporativo Prático -->
          <div class="flex flex-col gap-4 text-left">
            <span class="font-mono text-xs font-medium tracking-[0.2em] uppercase text-[var(--color-text-muted)]/60">
              Competências Práticas
            </span>
            <div class="sobre-comp gs-hidden bg-[var(--color-bg-surface)]/40 backdrop-blur-sm border border-[var(--color-border)] rounded-xl p-5 md:p-6 text-[var(--color-text-muted)] text-sm md:text-base leading-relaxed hover:border-[var(--color-ultraviolet)]/40 transition-colors duration-300">
              <p class="mb-4">
                Especialista na orquestração de <strong class="text-[var(--color-text-pure)] font-semibold">controle de inventário de resíduos</strong> e logística de devoluções diretamente no chão de fábrica.
              </p>
              <p>
                Desenvolvo lógicas estritas para <strong class="text-[var(--color-text-pure)] font-semibold">reconciliação de estoque</strong> em tempo real e <strong class="text-[var(--color-text-pure)] font-semibold">automação de processos</strong> industriais, mitigando perdas financeiras sistêmicas por meio de processamento em lote escalável.
              </p>
            </div>
          </div>

        </div>

      </div>
    </div>
  </section>
</template>
