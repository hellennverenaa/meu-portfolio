<script setup>
import { Mail } from '@lucide/vue'
</script>

<template>
  <!-- ═══════════ CONTATO ═══════════ -->
  <section id="contato" class="relative py-20 md:py-32 lg:py-40 px-4 md:px-12 lg:px-16 text-center">
    <div class="max-w-3xl mx-auto flex flex-col items-center gap-6 md:gap-10">
      <span class="contato-label gs-hidden font-mono text-xs font-medium tracking-[0.2em] uppercase text-[var(--color-magenta)]">
        § Contato
      </span>
      <h2 class="contato-title gs-hidden text-3xl sm:text-4xl md:text-5xl lg:text-8xl font-black tracking-brutal leading-[0.9] text-[var(--color-text-pure)]">
        Vamos construir
        <span class="block text-transparent bg-clip-text bg-gradient-to-r from-[var(--color-ultraviolet)] to-[var(--color-magenta)] mt-1 md:mt-2">o futuro.</span>
      </h2>

      <p class="contato-text gs-hidden text-base md:text-xl text-[var(--color-text-muted)] max-w-xl leading-relaxed">
        Aberta a oportunidades focadas em resolver problemas industriais
        complexos com código elegante e escalável.
      </p>

      <a
        href="mailto:hellen@example.com"
        class="contato-cta gs-hidden group mt-2 md:mt-4 inline-flex items-center gap-3 md:gap-4 px-8 md:px-10 py-4 md:py-5
               bg-[var(--color-ultraviolet)] text-white
               font-bold text-sm md:text-base tracking-wide
               rounded-full
               shadow-[0_4px_25px_rgba(112,0,255,0.35)]
               hover:bg-[var(--color-magenta)]
               hover:shadow-[0_8px_30px_rgba(255,0,127,0.45)] hover:-translate-y-1
               active:scale-95 active:translate-y-0
               focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-[var(--color-magenta)]/50
               transform-gpu transition-all duration-500 ease-[cubic-bezier(0.25,1,0.5,1)]"
      >
        <Mail class="w-4 md:w-5 h-4 md:h-5 group-hover:-rotate-12 transition-transform duration-300" />
        Iniciar Conversa
      </a>
    </div>
  </section>

  <!-- ═══════════ RODAPÉ ═══════════ -->
  <footer class="py-8 md:py-12 px-4 md:px-12 lg:px-16 border-t border-[var(--color-border)]">
    <div class="max-w-7xl mx-auto flex flex-col md:flex-row items-center justify-between gap-4 md:gap-6">
      <p class="font-mono text-[10px] md:text-xs text-[var(--color-text-muted)] tracking-wider">
        &copy; 2025 <strong class="text-[var(--color-text-pure)]">hellen.dev</strong>
      </p>
      <div class="flex gap-6 md:gap-8">
        <a href="https://github.com/" target="_blank" rel="noopener noreferrer"
           class="font-mono text-[10px] md:text-xs tracking-widest uppercase text-[var(--color-text-muted)] hover:text-[var(--color-magenta)] transition-colors duration-300">
          GitHub
        </a>
        <a href="https://linkedin.com/in/" target="_blank" rel="noopener noreferrer"
           class="font-mono text-[10px] md:text-xs tracking-widest uppercase text-[var(--color-text-muted)] hover:text-[var(--color-magenta)] transition-colors duration-300">
          LinkedIn
        </a>
      </div>
    </div>
  </footer>
</template>
