<script setup>
const ferramentas = [
  'Vue 3',
  'Node.js',
  'PostgreSQL',
  'Prisma ORM',
  'Tailwind CSS',
  'TypeScript',
  'Git',
  'REST API',
  'Lean / A3',
  'Vite',
]
</script>

<template>
  <div class="relative py-6 overflow-hidden border-y border-[var(--color-ultraviolet)]/20 bg-[var(--color-bg-main)]">
    <!-- Track dupla para loop contínuo -->
    <div class="marquee-track flex items-center gap-0 whitespace-nowrap w-max">
      <!-- Primeira cópia -->
      <template v-for="(tool, i) in ferramentas" :key="'a-' + i">
        <span class="font-mono text-sm font-medium tracking-wide text-[var(--color-text-muted)] px-8 hover:text-[var(--color-text-pure)] transition-colors duration-300">
          {{ tool }}
        </span>
        <span class="text-[var(--color-ultraviolet)]/40 text-xs select-none">§</span>
      </template>
      <!-- Segunda cópia (loop contínuo) -->
      <template v-for="(tool, i) in ferramentas" :key="'b-' + i">
        <span class="font-mono text-sm font-medium tracking-wide text-[var(--color-text-muted)] px-8 hover:text-[var(--color-text-pure)] transition-colors duration-300">
          {{ tool }}
        </span>
        <span class="text-[var(--color-ultraviolet)]/40 text-xs select-none">§</span>
      </template>
    </div>
  </div>
</template>
