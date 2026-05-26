<script setup>
// ─── Dados das Stacks por Categoria ─────────────────────────────────────────
const categorias = [
  {
    titulo: 'Frontend',
    descricao: 'Interfaces reativas e performáticas',
    icone: '◇',
    techs: [
      { nome: 'Vue 3', nivel: 'Avançado', destaque: true },
      { nome: 'TypeScript', nivel: 'Avançado', destaque: true },
      { nome: 'Tailwind CSS', nivel: 'Avançado', destaque: false },
      { nome: 'GSAP', nivel: 'Intermediário', destaque: false },
      { nome: 'Vite', nivel: 'Avançado', destaque: false },
    ]
  },
  {
    titulo: 'Backend',
    descricao: 'APIs robustas e escaláveis',
    icone: '⬡',
    techs: [
      { nome: 'Node.js', nivel: 'Avançado', destaque: true },
      { nome: 'Express', nivel: 'Avançado', destaque: false },
      { nome: 'Prisma ORM', nivel: 'Avançado', destaque: true },
      { nome: 'REST API', nivel: 'Avançado', destaque: false },
      { nome: 'JWT / Auth', nivel: 'Intermediário', destaque: false },
    ]
  },
  {
    titulo: 'Mobile',
    descricao: 'Apps nativos e multiplataforma',
    icone: '◈',
    techs: [
      { nome: 'React Native', nivel: 'Intermediário', destaque: false },
      { nome: 'Expo', nivel: 'Intermediário', destaque: false },
      { nome: 'Capacitor', nivel: 'Básico', destaque: false },
    ]
  },
  {
    titulo: 'Bancos de Dados',
    descricao: 'Modelagem e otimização de queries',
    icone: '⊡',
    techs: [
      { nome: 'PostgreSQL', nivel: 'Avançado', destaque: true },
      { nome: 'MySQL', nivel: 'Avançado', destaque: false },
      { nome: 'Redis', nivel: 'Intermediário', destaque: false },
      { nome: 'MongoDB', nivel: 'Intermediário', destaque: false },
    ]
  },
  {
    titulo: 'Cloud & DevOps',
    descricao: 'Deploy, CI/CD e infraestrutura',
    icone: '△',
    techs: [
      { nome: 'Git', nivel: 'Avançado', destaque: true },
      { nome: 'Docker', nivel: 'Intermediário', destaque: false },
      { nome: 'GitHub Actions', nivel: 'Intermediário', destaque: false },
      { nome: 'Vercel', nivel: 'Avançado', destaque: false },
      { nome: 'Linux', nivel: 'Intermediário', destaque: false },
    ]
  },
]

// Mapeia nível → cor do indicador
function corNivel(nivel) {
  if (nivel === 'Avançado') return 'bg-[var(--color-terminal)] shadow-[0_0_6px_rgba(57,255,20,0.4)]'
  if (nivel === 'Intermediário') return 'bg-[var(--color-ultraviolet)] shadow-[0_0_6px_rgba(112,0,255,0.4)]'
  return 'bg-[var(--color-text-muted)]/50'
}
</script>

<template>
  <!-- ═══════════ STACKS & FERRAMENTAS ═══════════ -->
  <section id="stacks" class="relative pt-10 pb-20 md:pt-16 md:pb-32 lg:pt-20 lg:pb-40 px-4 md:px-12 lg:px-16 scroll-mt-20">

    <div class="max-w-7xl mx-auto">

      <!-- Header da seção -->
      <div class="mb-16 md:mb-20">
        <span class="stacks-label font-mono text-xs font-medium tracking-[0.2em] uppercase text-[var(--color-magenta)] block mb-4">
          § Stacks & Ferramentas
        </span>
        <h2 class="stacks-title text-3xl sm:text-4xl md:text-5xl lg:text-7xl font-black tracking-brutal leading-[0.9] text-[var(--color-text-pure)]">
          A oficina,
          <span class="block text-transparent bg-clip-text bg-gradient-to-r from-[var(--color-ultraviolet)] to-[var(--color-magenta)] mt-1 md:mt-2">arrumada.</span>
        </h2>
        <p class="stacks-desc mt-6 text-base md:text-lg text-[var(--color-text-muted)] max-w-2xl leading-relaxed">
          Ferramentas que domino para transformar requisitos complexos em sistemas
          elegantes. Cada tecnologia foi escolhida por performance, ergonomia e
          aderência ao ecossistema industrial.
        </p>
      </div>

      <!-- Grid de Categorias -->
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4 md:gap-6">

        <div
          v-for="(cat, idx) in categorias"
          :key="cat.titulo"
          class="stacks-card group relative rounded-2xl border border-[var(--color-border)] bg-[var(--color-bg-surface)]/40 backdrop-blur-sm
                 hover:border-[var(--color-ultraviolet)]/40 hover:bg-[var(--color-bg-surface)]/60
                 hover:shadow-[0_0_40px_rgba(112,0,255,0.08)]
                 transition-all duration-500 ease-out overflow-hidden"
        >
          <!-- Glow sutil no hover -->
          <div class="absolute inset-0 bg-gradient-to-br from-[var(--color-ultraviolet)]/3 to-transparent opacity-0 group-hover:opacity-100 transition-opacity duration-500 pointer-events-none"></div>

          <div class="relative p-6 md:p-8">
            <!-- Cabeçalho do card -->
            <div class="flex items-center gap-3 mb-1">
              <span class="text-xl text-[var(--color-ultraviolet)] opacity-60 group-hover:opacity-100 transition-opacity duration-300">{{ cat.icone }}</span>
              <h3 class="font-mono text-sm font-bold uppercase tracking-widest text-[var(--color-text-pure)]">
                {{ cat.titulo }}
              </h3>
            </div>
            <p class="font-mono text-[10px] text-[var(--color-text-muted)] tracking-wider mb-6 pl-9">
              {{ cat.descricao }}
            </p>

            <!-- Lista de Tecnologias -->
            <div class="space-y-3">
              <div
                v-for="tech in cat.techs"
                :key="tech.nome"
                class="flex items-center justify-between gap-3 py-2 px-3 rounded-lg
                       border border-transparent hover:border-[var(--color-border)]
                       hover:bg-[var(--color-bg-surface)]/50
                       transition-all duration-300"
              >
                <div class="flex items-center gap-3">
                  <span
                    :class="[
                      'w-1.5 h-1.5 rounded-full flex-shrink-0 transition-all duration-300',
                      corNivel(tech.nivel)
                    ]"
                  ></span>
                  <span
                    :class="[
                      'text-sm font-medium transition-colors duration-300',
                      tech.destaque
                        ? 'text-[var(--color-text-pure)]'
                        : 'text-[var(--color-text-muted)]'
                    ]"
                  >
                    {{ tech.nome }}
                  </span>
                </div>
                <span class="font-mono text-[9px] uppercase tracking-widest text-[var(--color-text-muted)]/60">
                  {{ tech.nivel }}
                </span>
              </div>
            </div>
          </div>

          <!-- Linha inferior decorativa — pulsa no hover -->
          <div class="h-px w-full bg-gradient-to-r from-transparent via-[var(--color-ultraviolet)]/20 to-transparent group-hover:via-[var(--color-magenta)]/40 transition-all duration-500"></div>
        </div>

      </div>

      <!-- Legenda -->
      <div class="mt-10 flex flex-wrap items-center gap-6 font-mono text-[10px] text-[var(--color-text-muted)] tracking-wider uppercase">
        <div class="flex items-center gap-2">
          <span class="w-2 h-2 rounded-full bg-[var(--color-terminal)] shadow-[0_0_6px_rgba(57,255,20,0.4)]"></span>
          Avançado
        </div>
        <div class="flex items-center gap-2">
          <span class="w-2 h-2 rounded-full bg-[var(--color-ultraviolet)] shadow-[0_0_6px_rgba(112,0,255,0.4)]"></span>
          Intermediário
        </div>
        <div class="flex items-center gap-2">
          <span class="w-2 h-2 rounded-full bg-[var(--color-text-muted)]/50"></span>
          Básico
        </div>
      </div>

    </div>
  </section>
</template>
