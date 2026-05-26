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
  <div class="relative py-6 overflow-hidden border-y border-[#2E2B27]/50 bg-[#0F0E0C]">
    <!-- Track dupla para loop sem gap -->
    <div class="marquee-track flex items-center gap-0 whitespace-nowrap w-max">
      <!-- Primeira cópia -->
      <template v-for="(tool, i) in ferramentas" :key="'a-' + i">
        <span class="font-[family-name:var(--font-mono)] text-sm font-medium tracking-wide text-[#7A7570] px-8">
          {{ tool }}
        </span>
        <span class="text-[#C96442]/40 text-xs select-none">§</span>
      </template>
      <!-- Segunda cópia (loop contínuo) -->
      <template v-for="(tool, i) in ferramentas" :key="'b-' + i">
        <span class="font-[family-name:var(--font-mono)] text-sm font-medium tracking-wide text-[#7A7570] px-8">
          {{ tool }}
        </span>
        <span class="text-[#C96442]/40 text-xs select-none">§</span>
      </template>
    </div>
  </div>
</template>
