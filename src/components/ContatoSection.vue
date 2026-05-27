<script setup>
import { ref } from 'vue'

const FORM_ENDPOINT = import.meta.env.VITE_FORMSPREE_URL

// ─── Dados Reativos do Formulário ────────────────────────────────────────────
const nome = ref('')
const assunto = ref('')
const mensagem = ref('')

const isSubmitting = ref(false)
const submetidoComSucesso = ref(false)

// ─── Envio Assíncrono via API (Formspree) ──────────────────────────────────
async function enviarFormulario() {
  if (!FORM_ENDPOINT) {
    console.error('URL da API não configurada nas variáveis de ambiente.')
    return
  }

  if (isSubmitting.value) return
  isSubmitting.value = true

  // Extrai apenas o token final caso você tenha colocado a URL inteira na Vercel,
  // ou usa o valor puro se você colocou apenas a chave.
  const token = FORM_ENDPOINT.includes('/') ? FORM_ENDPOINT.split('/').pop() : FORM_ENDPOINT

  try {
    const response = await fetch('https://api.web3forms.com/submit', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
        'Accept': 'application/json',
      },
      body: JSON.stringify({
        access_key: token,
        name: nome.value,
        subject: assunto.value,
        message: mensagem.value,
      }),
    })

    const data = await response.json()

    if (response.ok && data.success) {
      submetidoComSucesso.value = true
      nome.value = ''
      assunto.value = ''
      mensagem.value = ''
    } else {
      console.error('Falha no envio do Web3Forms:', data.message || 'Erro desconhecido')
    }
  } catch (error) {
    console.error('Erro ao conectar com a API:', error)
  } finally {
    isSubmitting.value = false
  }
}

// ─── Links de Redes Sociais — cards descritivos ───────────────────────────────
const socialLinks = [
  {
    label:      'WhatsApp',
    sublabel:   '+55 75 98297-9829',
    href:       'https://wa.me/5575982979829',
    hoverClass: 'hover:border-green-500/60 hover:text-green-400 hover:shadow-[0_0_18px_rgba(34,197,94,0.2)]',
    icon: `<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round" class="w-5 h-5 shrink-0"><path d="M21 11.5a8.38 8.38 0 0 1-.9 3.8 8.5 8.5 0 0 1-7.6 4.7 8.38 8.38 0 0 1-3.8-.9L3 21l1.9-5.7a8.38 8.38 0 0 1-.9-3.8 8.5 8.5 0 0 1 4.7-7.6 8.38 8.38 0 0 1 3.8-.9h.5a8.48 8.48 0 0 1 8 8v.5z"/></svg>`,
  },
  {
    label:      'LinkedIn',
    sublabel:   'linkedin.com/in/hellen-verena',
    href:       'https://www.linkedin.com/in/hellen-verena/',
    hoverClass: 'hover:border-sky-500/60 hover:text-sky-400 hover:shadow-[0_0_18px_rgba(14,165,233,0.2)]',
    icon: `<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round" class="w-5 h-5 shrink-0"><path d="M16 8a6 6 0 0 1 6 6v7h-4v-7a2 2 0 0 0-2-2 2 2 0 0 0-2 2v7h-4v-7a6 6 0 0 1 6-6z"/><rect x="2" y="9" width="4" height="12"/><circle cx="4" cy="4" r="2"/></svg>`,
  },
  {
    label:      'GitHub',
    sublabel:   '@hellennverenaa',
    href:       'https://github.com/hellennverenaa',
    hoverClass: 'hover:border-neutral-400/60 hover:text-neutral-200 hover:shadow-[0_0_18px_rgba(200,200,200,0.15)]',
    icon: `<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round" class="w-5 h-5 shrink-0"><path d="M9 19c-5 1.5-5-2.5-7-3m14 6v-3.87a3.37 3.37 0 0 0-.94-2.61c3.14-.35 6.44-1.54 6.44-7A5.44 5.44 0 0 0 20 4.77 5.07 5.07 0 0 0 19.91 1S18.73.65 16 2.48a13.38 13.38 0 0 0-7 0C6.27.65 5.09 1 5.09 1A5.07 5.07 0 0 0 5 4.77a5.44 5.44 0 0 0-1.5 3.78c0 5.42 3.3 6.61 6.44 7A3.37 3.37 0 0 0 9 18.13V22"/></svg>`,
  },
  {
    label:      'Instagram',
    sublabel:   '@hellennverena',
    href:       'https://www.instagram.com/hellennverena/',
    hoverClass: 'hover:border-pink-500/60 hover:text-pink-400 hover:shadow-[0_0_18px_rgba(236,72,153,0.2)]',
    icon: `<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round" class="w-5 h-5 shrink-0"><rect x="2" y="2" width="20" height="20" rx="5" ry="5"/><path d="M16 11.37A4 4 0 1 1 12.63 8 4 4 0 0 1 16 11.37z"/><line x1="17.5" y1="6.5" x2="17.51" y2="6.5"/></svg>`,
  },
  {
    label:      'E-mail',
    sublabel:   'hellenverena20@gmail.com',
    href:       'mailto:hellenverena20@gmail.com',
    hoverClass: 'hover:border-[var(--color-magenta)]/60 hover:text-[var(--color-magenta)] hover:shadow-[0_0_18px_rgba(255,0,127,0.2)]',
    icon: `<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round" class="w-5 h-5 shrink-0"><path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"/><polyline points="22,6 12,13 2,6"/></svg>`,
  },
]
</script>

<template>
  <!-- ═══════════ CONTATO ═══════════ -->
  <section id="contato" class="relative py-20 md:py-32 lg:py-40 px-4 md:px-12 lg:px-16 scroll-mt-20">
    <div class="max-w-6xl mx-auto flex flex-col items-center gap-10 md:gap-14">

      <!-- ── Cabeçalho ─────────────────────────────────────────────────────── -->
      <div class="flex flex-col items-center gap-4 text-center">
        <span class="contato-label gs-hidden font-mono text-xs font-medium tracking-[0.2em] uppercase text-magenta">
          § Contato
        </span>
        <h2 class="contato-title gs-hidden text-3xl sm:text-4xl md:text-5xl lg:text-8xl font-black tracking-brutal leading-[0.9] text-(--color-text-pure)">
          Vamos construir
          <span class="block text-transparent bg-clip-text bg-linear-to-r from-ultraviolet to-magenta mt-1 md:mt-2">o futuro.</span>
        </h2>
        <p class="contato-text gs-hidden text-base md:text-xl text-(--color-text-muted) max-w-xl leading-relaxed">
          Aberta a oportunidades focadas em resolver problemas industriais
          complexos com código elegante e escalável.
        </p>
      </div>

      <!-- ── Painel duplo: Contatos | Formulário ──────────────────────────── -->
      <div class="contato-cta gs-hidden w-full grid grid-cols-1 lg:grid-cols-2 gap-8 lg:gap-14 items-start">

        <!-- ── Coluna Esquerda: Lista de Redes ─────────────────────────────── -->
        <div class="flex flex-col gap-3">
          <p class="font-mono text-[10px] uppercase tracking-[0.2em] text-(--color-text-muted) mb-1">
            Canais de contato
          </p>

          <a
            v-for="social in socialLinks"
            :key="social.label"
            :href="social.href"
            :aria-label="`${social.label}: ${social.sublabel}`"
            target="_blank"
            rel="noopener noreferrer"
            :class="[
              'group flex items-center gap-4 px-5 py-4 rounded-2xl',
              'border border-(--color-border) bg-(--color-bg-surface)/40',
              'text-(--color-text-muted) backdrop-blur-sm',
              'transition-all duration-300 transform-gpu hover:-translate-y-0.5 active:scale-[0.98]',
              social.hoverClass
            ]"
          >
            <!-- Ícone com aro de fundo sutil -->
            <span class="flex items-center justify-center w-10 h-10 rounded-xl bg-(--color-bg-surface)/60 border border-(--color-border) group-hover:border-current transition-colors duration-300 shrink-0"
                  v-html="social.icon" />

            <!-- Texto descritivo -->
            <span class="flex flex-col gap-0.5 min-w-0">
              <span class="font-mono text-[11px] uppercase tracking-[0.18em] text-(--color-text-muted) group-hover:text-current transition-colors duration-300">
                {{ social.label }}
              </span>
              <span class="font-mono text-sm font-medium text-(--color-text-pure) truncate">
                {{ social.sublabel }}
              </span>
            </span>

            <!-- Seta de navegação -->
            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"
                 class="w-4 h-4 ml-auto shrink-0 opacity-0 -translate-x-1 group-hover:opacity-100 group-hover:translate-x-0 transition-all duration-300">
              <path d="M7 17L17 7M17 7H7M17 7v10"/>
            </svg>
          </a>
        </div>

        <!-- ── Coluna Direita: Formulário ou Sucesso ───────────────────────── -->
        <div class="w-full">
          <form
            v-if="!submetidoComSucesso"
            @submit.prevent="enviarFormulario"
            class="flex flex-col gap-4 text-left"
            novalidate
          >
            <p class="font-mono text-[10px] uppercase tracking-[0.2em] text-(--color-text-muted) mb-1">
              Enviar mensagem
            </p>

            <!-- Nome -->
            <div class="flex flex-col gap-1.5">
              <label for="contato-nome" class="font-mono text-xs uppercase tracking-widest text-(--color-text-muted)">Nome</label>
              <input
                id="contato-nome"
                v-model="nome"
                type="text"
                placeholder="Seu nome"
                required
                class="w-full px-4 py-3 rounded-xl bg-(--color-bg-surface)/60 border border-(--color-border)
                       text-(--color-text-pure) font-mono text-sm placeholder:text-(--color-text-muted)/50
                       focus:outline-none focus:border-ultraviolet/60 focus:shadow-[0_0_12px_rgba(112,0,255,0.15)]
                       transition-all duration-300 backdrop-blur-sm"
              />
            </div>

            <!-- Assunto -->
            <div class="flex flex-col gap-1.5">
              <label for="contato-assunto" class="font-mono text-xs uppercase tracking-widest text-(--color-text-muted)">Assunto</label>
              <input
                id="contato-assunto"
                v-model="assunto"
                type="text"
                placeholder="Sobre o projeto..."
                required
                class="w-full px-4 py-3 rounded-xl bg-(--color-bg-surface)/60 border border-(--color-border)
                       text-(--color-text-pure) font-mono text-sm placeholder:text-(--color-text-muted)/50
                       focus:outline-none focus:border-ultraviolet/60 focus:shadow-[0_0_12px_rgba(112,0,255,0.15)]
                       transition-all duration-300 backdrop-blur-sm"
              />
            </div>

            <!-- Mensagem -->
            <div class="flex flex-col gap-1.5">
              <label for="contato-mensagem" class="font-mono text-xs uppercase tracking-widest text-(--color-text-muted)">Mensagem</label>
              <textarea
                id="contato-mensagem"
                v-model="mensagem"
                rows="5"
                placeholder="Descreva o desafio que quer resolver..."
                required
                class="w-full px-4 py-3 rounded-xl bg-(--color-bg-surface)/60 border border-(--color-border)
                       text-(--color-text-pure) font-mono text-sm placeholder:text-(--color-text-muted)/50
                       focus:outline-none focus:border-ultraviolet/60 focus:shadow-[0_0_12px_rgba(112,0,255,0.15)]
                       transition-all duration-300 backdrop-blur-sm resize-none"
              ></textarea>
            </div>

            <!-- Botão de envio -->
            <button
              type="submit"
              :disabled="isSubmitting"
              class="group inline-flex items-center justify-center gap-3 px-8 py-4 mt-1
                     bg-ultraviolet text-white font-bold text-sm tracking-wide
                     rounded-full shadow-[0_4px_25px_rgba(112,0,255,0.35)]
                     hover:bg-magenta hover:shadow-[0_8px_30px_rgba(255,0,127,0.45)] hover:-translate-y-1
                     active:scale-95 active:translate-y-0
                     focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-magenta/50
                     disabled:opacity-75 disabled:cursor-not-allowed disabled:hover:translate-y-0 disabled:hover:shadow-[0_4px_25px_rgba(112,0,255,0.35)]
                     transform-gpu transition-all duration-500 ease-[cubic-bezier(0.25,1,0.5,1)]"
            >
              <!-- SVG de Enviar ou Spinner de Carregamento -->
              <svg
                v-if="!isSubmitting"
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 24 24"
                fill="none"
                stroke="currentColor"
                stroke-width="2"
                stroke-linecap="round"
                stroke-linejoin="round"
                class="w-4 h-4 group-hover:-rotate-12 transition-transform duration-300"
              >
                <path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"/>
                <polyline points="22,6 12,13 2,6"/>
              </svg>
              <svg
                v-else
                class="animate-spin h-4 w-4 text-white"
                xmlns="http://www.w3.org/2000/svg"
                fill="none"
                viewBox="0 0 24 24"
              >
                <circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4"></circle>
                <path class="opacity-75" fill="currentColor" d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"></path>
              </svg>
              {{ isSubmitting ? 'Enviando...' : 'Enviar Mensagem' }}
            </button>

            <!-- Nota de rodapé discreta -->
            <p class="font-mono text-[10px] text-(--color-text-muted)/50 text-center">
              Sua mensagem será enviada com segurança e de forma assíncrona.
            </p>
          </form>

          <!-- Mensagem Elegante de Sucesso no Estilo Acheron -->
          <div
            v-else
            class="flex flex-col items-center justify-center p-8 md:p-12 text-center
                   bg-(--color-bg-surface)/40 backdrop-blur-2xl
                   border border-(--color-border)
                   rounded-2xl shadow-[0_8px_40px_rgba(255,0,127,0.15)]
                   relative overflow-hidden min-h-87.5
                   transform-gpu transition-all duration-500 ease-[cubic-bezier(0.25,1,0.5,1)]"
          >
            <!-- Borda superior neon magenta -->
            <div class="absolute top-0 left-0 right-0 h-px bg-linear-to-r from-transparent via-magenta to-transparent"></div>
            
            <!-- Glow sutil de fundo (neon verde) -->
            <div class="absolute inset-0 bg-linear-to-b from-terminal/5 to-transparent pointer-events-none"></div>

            <!-- Ícone de checkmark com glow neon verde -->
            <div class="w-16 h-16 flex items-center justify-center rounded-full bg-terminal/10 text-terminal border border-terminal/25 mb-6 shadow-[0_0_20px_rgba(57,255,20,0.2)]">
              <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round" class="w-8 h-8">
                <polyline points="20 6 9 17 4 12" />
              </svg>
            </div>

            <p class="font-mono text-[10px] uppercase tracking-[0.25em] text-(--color-text-muted) mb-3">
              § Status: Enviado
            </p>

            <h3 class="text-xl md:text-2xl font-bold tracking-tight text-center max-w-sm leading-relaxed">
              <span class="text-transparent bg-clip-text bg-linear-to-r from-terminal to-magenta filter drop-shadow-[0_0_10px_rgba(57,255,20,0.35)]">
                Mensagem enviada com sucesso! Entrarei em contato em breve.
              </span>
            </h3>
          </div>
        </div>

      </div><!-- fim grid -->
    </div>
  </section>

  <!-- ═══════════ RODAPÉ ═══════════ -->
  <footer class="py-8 md:py-12 px-4 md:px-12 lg:px-16 border-t border-(--color-border)">
    <div class="max-w-7xl mx-auto flex flex-col md:flex-row items-center justify-between gap-4 md:gap-6">
      <p class="font-mono text-[10px] md:text-xs text-(--color-text-muted) tracking-wider">
        &copy; 2026 <strong class="text-(--color-text-pure)">hellen.dev</strong>
      </p>
      <div class="flex gap-6 md:gap-8">
        <a href="https://github.com/hellennverenaa" target="_blank" rel="noopener noreferrer"
           class="font-mono text-[10px] md:text-xs tracking-widest uppercase text-(--color-text-muted) hover:text-magenta transition-colors duration-300">
          GitHub
        </a>
        <a href="https://www.linkedin.com/in/hellen-verena/" target="_blank" rel="noopener noreferrer"
           class="font-mono text-[10px] md:text-xs tracking-widest uppercase text-(--color-text-muted) hover:text-magenta transition-colors duration-300">
          LinkedIn
        </a>
        <a href="https://www.instagram.com/hellennverena/" target="_blank" rel="noopener noreferrer"
           class="font-mono text-[10px] md:text-xs tracking-widest uppercase text-(--color-text-muted) hover:text-magenta transition-colors duration-300">
          Instagram
        </a>
        <a href="https://wa.me/5575982979829" target="_blank" rel="noopener noreferrer"
           class="font-mono text-[10px] md:text-xs tracking-widest uppercase text-(--color-text-muted) hover:text-magenta transition-colors duration-300">
          WhatsApp
        </a>
      </div>
    </div>
  </footer>
</template>
