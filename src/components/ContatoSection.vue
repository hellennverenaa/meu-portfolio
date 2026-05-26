<script setup>
// ─── Ícones SVG inline para redes sociais ───────────────────────────────────
const socialLinks = [
  {
    label: 'Instagram',
    href: 'https://www.instagram.com/hellennverena/',
    icon: `<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round" class="w-5 h-5"><rect x="2" y="2" width="20" height="20" rx="5" ry="5"/><path d="M16 11.37A4 4 0 1 1 12.63 8 4 4 0 0 1 16 11.37z"/><line x1="17.5" y1="6.5" x2="17.51" y2="6.5"/></svg>`,
  },
  {
    label: 'LinkedIn',
    href: 'https://www.linkedin.com/in/hellen-verena/',
    icon: `<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round" class="w-5 h-5"><path d="M16 8a6 6 0 0 1 6 6v7h-4v-7a2 2 0 0 0-2-2 2 2 0 0 0-2 2v7h-4v-7a6 6 0 0 1 6-6z"/><rect x="2" y="9" width="4" height="12"/><circle cx="4" cy="4" r="2"/></svg>`,
  },
  {
    label: 'GitHub',
    href: 'https://github.com/hellennverenaa',
    icon: `<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round" class="w-5 h-5"><path d="M9 19c-5 1.5-5-2.5-7-3m14 6v-3.87a3.37 3.37 0 0 0-.94-2.61c3.14-.35 6.44-1.54 6.44-7A5.44 5.44 0 0 0 20 4.77 5.07 5.07 0 0 0 19.91 1S18.73.65 16 2.48a13.38 13.38 0 0 0-7 0C6.27.65 5.09 1 5.09 1A5.07 5.07 0 0 0 5 4.77a5.44 5.44 0 0 0-1.5 3.78c0 5.42 3.3 6.61 6.44 7A3.37 3.37 0 0 0 9 18.13V22"/></svg>`,
  },
  {
    label: 'WhatsApp',
    href: 'https://wa.me/5575982979829',
    icon: `<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round" class="w-5 h-5"><path d="M21 11.5a8.38 8.38 0 0 1-.9 3.8 8.5 8.5 0 0 1-7.6 4.7 8.38 8.38 0 0 1-3.8-.9L3 21l1.9-5.7a8.38 8.38 0 0 1-.9-3.8 8.5 8.5 0 0 1 4.7-7.6 8.38 8.38 0 0 1 3.8-.9h.5a8.48 8.48 0 0 1 8 8v.5z"/></svg>`,
  },
]
</script>

<template>
  <!-- ═══════════ CONTATO ═══════════ -->
  <section id="contato" class="relative py-20 md:py-32 lg:py-40 px-4 md:px-12 lg:px-16 text-center scroll-mt-20">
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

      <!-- Formulário de contato -->
      <form
        action="mailto:hellen@example.com"
        method="GET"
        enctype="text/plain"
        class="contato-cta gs-hidden w-full max-w-lg flex flex-col gap-4 text-left mt-2"
      >
        <div class="flex flex-col gap-1.5">
          <label for="contato-nome" class="font-mono text-xs uppercase tracking-widest text-[var(--color-text-muted)]">Nome</label>
          <input
            id="contato-nome"
            name="nome"
            type="text"
            placeholder="Seu nome"
            class="w-full px-4 py-3 rounded-xl bg-[var(--color-bg-surface)]/60 border border-[var(--color-border)]
                   text-[var(--color-text-pure)] font-mono text-sm placeholder:text-[var(--color-text-muted)]/50
                   focus:outline-none focus:border-[var(--color-ultraviolet)]/60 focus:shadow-[0_0_12px_rgba(112,0,255,0.15)]
                   transition-all duration-300 backdrop-blur-sm"
          />
        </div>
        <div class="flex flex-col gap-1.5">
          <label for="contato-assunto" class="font-mono text-xs uppercase tracking-widest text-[var(--color-text-muted)]">Assunto</label>
          <input
            id="contato-assunto"
            name="subject"
            type="text"
            placeholder="Sobre o projeto..."
            class="w-full px-4 py-3 rounded-xl bg-[var(--color-bg-surface)]/60 border border-[var(--color-border)]
                   text-[var(--color-text-pure)] font-mono text-sm placeholder:text-[var(--color-text-muted)]/50
                   focus:outline-none focus:border-[var(--color-ultraviolet)]/60 focus:shadow-[0_0_12px_rgba(112,0,255,0.15)]
                   transition-all duration-300 backdrop-blur-sm"
          />
        </div>
        <div class="flex flex-col gap-1.5">
          <label for="contato-mensagem" class="font-mono text-xs uppercase tracking-widest text-[var(--color-text-muted)]">Mensagem</label>
          <textarea
            id="contato-mensagem"
            name="body"
            rows="4"
            placeholder="Descreva o desafio que quer resolver..."
            class="w-full px-4 py-3 rounded-xl bg-[var(--color-bg-surface)]/60 border border-[var(--color-border)]
                   text-[var(--color-text-pure)] font-mono text-sm placeholder:text-[var(--color-text-muted)]/50
                   focus:outline-none focus:border-[var(--color-ultraviolet)]/60 focus:shadow-[0_0_12px_rgba(112,0,255,0.15)]
                   transition-all duration-300 backdrop-blur-sm resize-none"
          ></textarea>
        </div>
        <button
          type="submit"
          class="group inline-flex items-center justify-center gap-3 px-8 py-4
                 bg-[var(--color-ultraviolet)] text-white font-bold text-sm tracking-wide
                 rounded-full shadow-[0_4px_25px_rgba(112,0,255,0.35)]
                 hover:bg-[var(--color-magenta)] hover:shadow-[0_8px_30px_rgba(255,0,127,0.45)] hover:-translate-y-1
                 active:scale-95 active:translate-y-0
                 focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-[var(--color-magenta)]/50
                 transform-gpu transition-all duration-500 ease-[cubic-bezier(0.25,1,0.5,1)]"
        >
          <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="w-4 h-4 group-hover:-rotate-12 transition-transform duration-300">
            <path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"/>
            <polyline points="22,6 12,13 2,6"/>
          </svg>
          Iniciar Conversa
        </button>
      </form>

      <!-- Redes Sociais -->
      <div class="contato-cta gs-hidden flex items-center gap-5 mt-2">
        <a
          v-for="social in socialLinks"
          :key="social.label"
          :href="social.href"
          :aria-label="social.label"
          target="_blank"
          rel="noopener noreferrer"
          class="group p-3 rounded-full border border-[var(--color-border)] bg-[var(--color-bg-surface)]/40
                 text-[var(--color-text-muted)] hover:text-[var(--color-magenta)]
                 hover:border-[var(--color-magenta)]/50 hover:shadow-[0_0_16px_rgba(255,0,127,0.2)]
                 backdrop-blur-sm transition-all duration-300 transform-gpu hover:scale-110 active:scale-95"
          v-html="social.icon"
        />
      </div>
    </div>
  </section>

  <!-- ═══════════ RODAPÉ ═══════════ -->
  <footer class="py-8 md:py-12 px-4 md:px-12 lg:px-16 border-t border-[var(--color-border)]">
    <div class="max-w-7xl mx-auto flex flex-col md:flex-row items-center justify-between gap-4 md:gap-6">
      <p class="font-mono text-[10px] md:text-xs text-[var(--color-text-muted)] tracking-wider">
        &copy; 2026 <strong class="text-[var(--color-text-pure)]">hellen.dev</strong>
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
        <a href="https://instagram.com/" target="_blank" rel="noopener noreferrer"
           class="font-mono text-[10px] md:text-xs tracking-widest uppercase text-[var(--color-text-muted)] hover:text-[var(--color-magenta)] transition-colors duration-300">
          Instagram
        </a>
        <a href="https://wa.me/55" target="_blank" rel="noopener noreferrer"
           class="font-mono text-[10px] md:text-xs tracking-widest uppercase text-[var(--color-text-muted)] hover:text-[var(--color-magenta)] transition-colors duration-300">
          WhatsApp
        </a>
      </div>
    </div>
  </footer>
</template>
