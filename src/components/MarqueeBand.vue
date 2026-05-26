<script setup>
const ferramentas = [
  'PostgreSQL',
  'Prisma ORM',
  'Vue 3',
  'Node.js',
  'Tailwind v4'
]
</script>

<template>
  <div class="relative py-6 overflow-hidden border-y border-[var(--color-border)] bg-[var(--color-bg-surface)]/20 backdrop-blur-md">
    <!-- Efeito de desbotamento nas laterais -->
    <div class="absolute inset-y-0 left-0 w-16 md:w-32 bg-gradient-to-r from-[var(--color-bg-main)] to-transparent z-10 pointer-events-none"></div>
    <div class="absolute inset-y-0 right-0 w-16 md:w-32 bg-gradient-to-l from-[var(--color-bg-main)] to-transparent z-10 pointer-events-none"></div>

    <div class="marquee-track flex items-center whitespace-nowrap">
      <!-- Primeira cópia -->
      <div class="flex items-center gap-12 md:gap-20 shrink-0 pr-12 md:pr-20">
        <div v-for="(tool, i) in ferramentas" :key="'a-' + i" class="flex items-center gap-3 md:gap-4 font-mono text-sm md:text-base font-bold tracking-wider text-[var(--color-text-muted)] hover:text-[var(--color-magenta)] transition-colors duration-300">
          <span>{{ tool }}</span>
          <span class="text-[var(--color-ultraviolet)] select-none opacity-50">✦</span>
        </div>
      </div>
      <!-- Segunda cópia -->
      <div class="flex items-center gap-12 md:gap-20 shrink-0 pr-12 md:pr-20">
        <div v-for="(tool, i) in ferramentas" :key="'b-' + i" class="flex items-center gap-3 md:gap-4 font-mono text-sm md:text-base font-bold tracking-wider text-[var(--color-text-muted)] hover:text-[var(--color-magenta)] transition-colors duration-300">
          <span>{{ tool }}</span>
          <span class="text-[var(--color-ultraviolet)] select-none opacity-50">✦</span>
        </div>
      </div>
      <!-- Terceira cópia -->
      <div class="flex items-center gap-12 md:gap-20 shrink-0 pr-12 md:pr-20">
        <div v-for="(tool, i) in ferramentas" :key="'c-' + i" class="flex items-center gap-3 md:gap-4 font-mono text-sm md:text-base font-bold tracking-wider text-[var(--color-text-muted)] hover:text-[var(--color-magenta)] transition-colors duration-300">
          <span>{{ tool }}</span>
          <span class="text-[var(--color-ultraviolet)] select-none opacity-50">✦</span>
        </div>
      </div>
      <!-- Quarta cópia -->
      <div class="flex items-center gap-12 md:gap-20 shrink-0 pr-12 md:pr-20">
        <div v-for="(tool, i) in ferramentas" :key="'d-' + i" class="flex items-center gap-3 md:gap-4 font-mono text-sm md:text-base font-bold tracking-wider text-[var(--color-text-muted)] hover:text-[var(--color-magenta)] transition-colors duration-300">
          <span>{{ tool }}</span>
          <span class="text-[var(--color-ultraviolet)] select-none opacity-50">✦</span>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.marquee-track {
  display: flex;
  width: max-content;
  animation: marquee-scroll 25s linear infinite;
}
.marquee-track:hover {
  animation-play-state: paused;
}
@keyframes marquee-scroll {
  0% {
    transform: translateX(0);
  }
  100% {
    transform: translateX(-50%);
  }
}
</style>
