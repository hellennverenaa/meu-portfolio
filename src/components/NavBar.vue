<script setup>
import { ref, computed } from 'vue'
import { Sun, Moon } from '@lucide/vue'

const modoEscuro = ref(true)

function alternarTema() {
  modoEscuro.value = !modoEscuro.value
  document.documentElement.classList.toggle('dark', modoEscuro.value)
}

function irPara(id) {
  document.getElementById(id)?.scrollIntoView({ behavior: 'smooth' })
}

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
</script>

<template>
  <header
    :class="[
      'fixed top-0 inset-x-0 z-50 transition-all duration-500 ease-out',
      'flex items-center justify-between px-6 md:px-12 lg:px-16',
      headerOpaco
        ? 'py-4 bg-[var(--color-bg-main)]/90 backdrop-blur-2xl border-b border-[var(--color-border)]/50'
        : 'py-8 bg-transparent border-b border-transparent'
    ]"
  >
    <!-- Logo -->
    <a
      href="#"
      @click.prevent="irPara('inicio')"
      class="group flex items-baseline gap-0.5 cursor-pointer"
    >
      <span class="text-xl font-bold tracking-tighter text-[var(--color-text-pure)] group-hover:text-[var(--color-magenta)] transition-colors duration-300">
        hellen
      </span>
      <span class="font-mono text-xs text-[var(--color-text-muted)] group-hover:text-[var(--color-magenta)]/60 transition-colors duration-300">
        .dev
      </span>
    </a>

    <!-- Nav central -->
    <nav class="hidden md:flex items-center gap-10">
      <a
        v-for="item in [
          { label: 'Sobre', id: 'sobre' },
          { label: 'Serviços', id: 'servicos' },
          { label: 'Projetos', id: 'projetos' },
          { label: 'Carreira', id: 'carreira' },
          { label: 'Contato', id: 'contato' },
        ]"
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
    <div class="flex items-center gap-4">
      <button
        @click="alternarTema"
        aria-label="Alternar tema"
        class="p-2.5 rounded-full
               border border-[var(--color-border)] bg-transparent
               text-[var(--color-text-muted)] hover:text-[var(--color-magenta)] hover:border-[var(--color-magenta)]/40
               active:scale-90
               focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-[var(--color-magenta)]/50
               transform-gpu transition-all duration-300 ease-out cursor-pointer"
      >
        <Sun v-if="modoEscuro" class="w-4 h-4" />
        <Moon v-else class="w-4 h-4" />
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
</template>
