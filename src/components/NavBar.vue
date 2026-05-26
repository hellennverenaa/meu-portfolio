<script setup>
import { ref, computed } from 'vue'
import { Sun, Moon, Menu, X } from '@lucide/vue'

// ─── Estado do Tema ─────────────────────────────────────────────────────────
const modoEscuro = ref(document.documentElement.classList.contains('dark'))

function alternarTema() {
  // Ativa transição suave de tema
  document.documentElement.classList.add('theme-transitioning')

  modoEscuro.value = !modoEscuro.value
  document.documentElement.classList.toggle('dark', modoEscuro.value)

  // Remove a classe de transição após a animação
  setTimeout(() => {
    document.documentElement.classList.remove('theme-transitioning')
  }, 500)
}

// ─── Menu Mobile ────────────────────────────────────────────────────────────
const menuAberto = ref(false)

function toggleMenu() {
  menuAberto.value = !menuAberto.value
}

function irPara(id) {
  menuAberto.value = false
  document.getElementById(id)?.scrollIntoView({ behavior: 'smooth' })
}

// ─── Props & Computeds ──────────────────────────────────────────────────────
const props = defineProps({
  scrollY: { type: Number, default: 0 }
})

const headerOpaco = computed(() => props.scrollY > 80)

const progressoLeitura = computed(() => {
  if (typeof window === 'undefined') return 0
  const total = document.body.scrollHeight - window.innerHeight
  if (total <= 0) return 0
  return Math.min((props.scrollY / total) * 100, 100)
})

const navItems = [
  { label: 'Sobre', id: 'sobre' },
  { label: 'Serviços', id: 'servicos' },
  { label: 'Projetos', id: 'projetos' },
  { label: 'Carreira', id: 'carreira' },
  { label: 'Contato', id: 'contato' },
]
</script>

<template>
  <header
    :class="[
      'fixed top-0 inset-x-0 z-50 transition-all duration-500 ease-out',
      'flex items-center justify-between px-4 md:px-12 lg:px-16',
      headerOpaco
        ? 'py-3 md:py-4 bg-[var(--color-bg-main)]/90 backdrop-blur-2xl border-b border-[var(--color-border)]/50 shadow-[0_4px_20px_rgba(0,0,0,0.1)]'
        : 'py-5 md:py-8 bg-transparent border-b border-transparent'
    ]"
  >
    <!-- Logo -->
    <a
      href="#"
      @click.prevent="irPara('inicio')"
      class="group flex items-baseline gap-0.5 cursor-pointer z-10"
    >
      <span class="text-lg md:text-xl font-bold tracking-tighter text-[var(--color-text-pure)] group-hover:text-[var(--color-magenta)] transition-colors duration-300">
        hellen
      </span>
      <span class="font-mono text-[10px] md:text-xs text-[var(--color-text-muted)] group-hover:text-[var(--color-magenta)]/60 transition-colors duration-300">
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
               text-[var(--color-text-muted)] hover:text-[var(--color-text-pure)]
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
               text-[var(--color-text-muted)] hover:text-[var(--color-magenta)] hover:border-[var(--color-magenta)]/40
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
               text-[var(--color-text-muted)] hover:text-[var(--color-magenta)]
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
      class="fixed inset-0 z-40 bg-[var(--color-bg-main)]/95 backdrop-blur-xl flex flex-col items-center justify-center gap-8 md:hidden"
    >
      <a
        v-for="item in navItems"
        :key="'mobile-' + item.id"
        :href="'#' + item.id"
        @click.prevent="irPara(item.id)"
        class="font-mono text-lg font-medium tracking-widest uppercase
               text-[var(--color-text-muted)] hover:text-[var(--color-magenta)]
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
