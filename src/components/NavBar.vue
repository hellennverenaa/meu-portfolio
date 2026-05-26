<script setup>
import { ref, computed } from 'vue'
import { Sun, Moon, Menu, X } from '@lucide/vue'

// ─── Estado do Tema ─────────────────────────────────────────────────────────
const modoEscuro = ref(document.documentElement.classList.contains('dark'))

function alternarTema() {
  document.documentElement.classList.add('theme-transitioning')
  modoEscuro.value = !modoEscuro.value
  document.documentElement.classList.toggle('dark', modoEscuro.value)
  setTimeout(() => {
    document.documentElement.classList.remove('theme-transitioning')
  }, 500)
}

// ─── Menu Mobile ────────────────────────────────────────────────────────────
const menuAberto = ref(false)

function toggleMenu() {
  menuAberto.value = !menuAberto.value
}

// ─── Navegação com offset para compensar navbar fixa + GSAP pin-spacer ─────
function irPara(id) {
  menuAberto.value = false

  // Caso especial: 'inicio' precisa ir para o topo absoluto da página,
  // porque o GSAP pin-spacer desloca o elemento #inicio do DOM original.
  if (id === 'inicio') {
    window.scrollTo({ top: 0, behavior: 'smooth' })
    return
  }

  const el = document.getElementById(id)
  if (!el) return

  // Calcula posição manual com offset da navbar (80px)
  // Isso evita que scrollIntoView fique escondido atrás da navbar fixa
  const navbarHeight = 80
  const elementTop = el.getBoundingClientRect().top + window.scrollY - navbarHeight
  window.scrollTo({ top: elementTop, behavior: 'smooth' })
}

// ─── Props & Computeds ──────────────────────────────────────────────────────
const props = defineProps({
  scrollY: { type: Number, default: 0 }
})



const progressoLeitura = computed(() => {
  if (typeof window === 'undefined') return 0
  const total = document.body.scrollHeight - window.innerHeight
  if (total <= 0) return 0
  return Math.min((props.scrollY / total) * 100, 100)
})

// Ordem: INÍCIO, SOBRE, CARREIRA, PROJETOS, STACKS, CONTATO
const navItems = [
  { label: 'INÍCIO', id: 'inicio' },
  { label: 'SOBRE', id: 'sobre' },
  { label: 'CARREIRA', id: 'carreira' },
  { label: 'PROJETOS', id: 'projetos' },
  { label: 'STACKS', id: 'stacks' },
  { label: 'CONTATO', id: 'contato' },
]
</script>

<template>
  <!-- Navbar — z-[100] garante que fique acima do GSAP pin-spacer (z-auto) -->
  <header class="fixed top-0 inset-x-0 z-[100] flex items-center justify-between px-4 md:px-12 lg:px-16 py-3 md:py-4 bg-white/80 dark:bg-[#06020D]/80 backdrop-blur-md border-b border-[var(--color-border)]/50">
    <!-- Logo -->
    <a
      href="#"
      @click.prevent="irPara('inicio')"
      class="group flex items-baseline gap-0.5 cursor-pointer z-10"
    >
      <span class="text-lg md:text-xl font-bold tracking-tighter text-neutral-900 dark:text-neutral-300 group-hover:text-[var(--color-magenta)] transition-colors duration-300">
        hellen
      </span>
      <span class="font-mono text-[10px] md:text-xs text-neutral-900 dark:text-neutral-300 group-hover:text-[var(--color-magenta)]/60 transition-colors duration-300">
        .dev
      </span>
    </a>

    <!-- Nav central — Desktop -->
    <nav class="hidden md:flex items-center gap-8 lg:gap-10">
      <a
        v-for="item in navItems"
        :key="item.id"
        :href="'#' + item.id"
        @click.prevent="irPara(item.id)"
        class="relative font-mono text-xs font-medium tracking-widest uppercase
               text-neutral-900 dark:text-neutral-300 hover:text-[var(--color-magenta)] dark:hover:text-white
               transition-colors duration-300
               after:absolute after:-bottom-1 after:left-0 after:w-0 after:h-px after:bg-[var(--color-magenta)]
               hover:after:w-full after:transition-all after:duration-500 after:ease-[cubic-bezier(0.25,1,0.5,1)]"
      >
        {{ item.label }}
      </a>
    </nav>

    <!-- Controles -->
    <div class="flex items-center gap-2 md:gap-4 z-10">
      <!-- Toggle de Tema -->
      <button
        @click="alternarTema"
        aria-label="Alternar tema claro/escuro"
        class="p-2 md:p-2.5 rounded-full
               border border-[var(--color-border)] bg-[var(--color-bg-surface)]/50
               text-neutral-900 dark:text-neutral-300 hover:text-[var(--color-magenta)] hover:border-[var(--color-magenta)]/40
               active:scale-90
               focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-[var(--color-magenta)]/50
               transform-gpu transition-all duration-300 ease-out cursor-pointer backdrop-blur-sm"
      >
        <Sun v-if="modoEscuro" class="w-4 h-4" />
        <Moon v-else class="w-4 h-4" />
      </button>

      <!-- Botão Menu Mobile -->
      <button
        @click="toggleMenu"
        aria-label="Menu de navegação"
        class="md:hidden p-2 rounded-full
               border border-[var(--color-border)] bg-[var(--color-bg-surface)]/50
               text-neutral-900 dark:text-neutral-300 hover:text-[var(--color-magenta)]
               active:scale-90
               focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-[var(--color-magenta)]/50
               transform-gpu transition-all duration-300 cursor-pointer backdrop-blur-sm"
      >
        <X v-if="menuAberto" class="w-4 h-4" />
        <Menu v-else class="w-4 h-4" />
      </button>
    </div>

    <!-- Barra de progresso de leitura — gradiente Ultravioleta → Magenta -->
    <div
      class="absolute bottom-0 left-0 h-px transition-all duration-150 ease-out"
      :style="{
        width: `${progressoLeitura}%`,
        background: 'linear-gradient(to right, var(--color-ultraviolet), var(--color-magenta))'
      }"
    />
  </header>

  <!-- Menu Mobile Overlay -->
  <Transition name="mobile-menu">
    <div
      v-if="menuAberto"
      class="fixed inset-0 z-[90] bg-[var(--color-bg-main)]/95 backdrop-blur-xl flex flex-col items-center justify-center gap-8 md:hidden"
    >
      <a
        v-for="item in navItems"
        :key="'mobile-' + item.id"
        :href="'#' + item.id"
        @click.prevent="irPara(item.id)"
        class="font-mono text-lg font-medium tracking-widest uppercase
               text-neutral-900 dark:text-neutral-300 hover:text-[var(--color-magenta)] dark:hover:text-white
               transition-colors duration-300"
      >
        {{ item.label }}
      </a>
    </div>
  </Transition>
</template>

<style scoped>
.mobile-menu-enter-active,
.mobile-menu-leave-active {
  transition: opacity 0.3s ease, transform 0.3s ease;
}

.mobile-menu-enter-from,
.mobile-menu-leave-to {
  opacity: 0;
  transform: translateY(-10px);
}
</style>
