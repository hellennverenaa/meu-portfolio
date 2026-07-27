<script setup>
import {
  Database,
  Scissors,
  GraduationCap,
  Settings,
  Layout,
  Factory,
  Globe,
  ExternalLink,
  Heart
} from '@lucide/vue'

// ─── Lista de Projetos — Atualizada em feature/atualizacao-projetos ─────────
// SCALE removido. Substituído pelo ERP Chão de Fábrica (Modelagem).
// Card de Casamentos Digitais inserido ao final do grid.
const projetos = [
  {
    id: 'erp-modelagem',
    nome: 'ERP Chão de Fábrica (Modelagem)',
    icone: Factory,
    problema:
      'Falta de rastreabilidade no chão de fábrica, descontrole em testes de qualidade/laboratório e comunicação descentralizada entre os setores de modelagem, gerando retrabalho e perda de peças sem histórico auditável.',
    arquitetura:
      'Arquitetura relacional robusta com 35 tabelas em PostgreSQL, backend em Node.js/TypeORM com RBAC dinâmico "Zero Hardcode" e integração a serviços legados via rede Docker isolada. Frontend em Vue 3 com bipagem de peças via RFID em Modo Quiosque, lógica de Handoff Automático entre setores e automação de e-mails/Dossiês em PDF.',
    pilha: ['Vue 3', 'Node.js', 'PostgreSQL', 'Docker', 'Tailwind v4', 'JWT Authentication', 'TypeScript', 'WebSockets (Socket.io)', 'Puppeteer', 'Axios', 'TypeORM',
      'Express.js', 'Helmet & Express Rate Limit', 'Swagger / OpenAPI 3.0', 'Zod', 'JWT (JSON Web Tokens) & Bcrypt', 'ntegração RFID / Modo Quiosque'
    ],
    categoria: 'ERP em Modelagem',
    destaque: true,
    link: null,
    imagem: null,
  },
  {
    id: 'sic',
    nome: 'SIC (Sistema Informativo de Comunicados)',
    icone: Settings,
    problema:
      'Entrega de alta urgência solicitada pela gestão para mitigar falhas de comunicação e desvio de informações críticas entre unidades produtivas.',
    arquitetura:
      'Sistema automatizado de comunicação no chão de fábrica. Robô que captura e-mails de modelagem da unidade Sul, processa os dados em banco centralizado e dispara alertas para um Dashboard. Interface acessada pelos operadores bipando o QR Code de cada modelo na linha de produção.',
    pilha: ['JavaScript', 'Google Apps Script', 'Automação', 'QR Code'],
    categoria: 'Projeto em Produção',
    destaque: true,
    link: null,
    imagem: null,
  },
  {
    id: 'sobracorte',
    nome: 'SobraCorte',
    icone: Scissors,
    problema:
      'Perda de rastreabilidade nas sobras físicas de lotes de corte e acumulação desordenada de cones de linha vazios no almoxarifado.',
    arquitetura:
      'Módulo web reativo em Vue 3 para processamento em lote de saldos de matéria-prima e gestão em tempo real do inventário de cones e devoluções ao estoque central.',
    pilha: ['Vue 3', 'Tailwind CSS', 'Inventário', 'PostgreSQL', 'REST API', 'Docker', 'JWT Authentication','Node.js'],
    categoria: 'Projeto Corporativo',
    destaque: false,
    link: null,
    imagem: null,
  },
  {
    id: 'almoxarifado',
    nome: 'Portal do Almoxarifado',
    icone: Layout,
    problema:
      'Processo de auditoria física de estoque lento, dependente de papelada física e preenchimento de planilhas manuais suscetíveis a erro humano.',
    arquitetura:
      'Dashboard responsivo e automatizado criado para ser operado via Tablet no centro de distribuição. Permite auditorias de estoque em tempo real e alimenta um painel central de controle na nuvem de forma automática.',
    pilha: ['JavaScript', 'Google Apps Script', 'UI/UX Mobile', 'Tablet First'],
    categoria: 'Projeto em Produção',
    destaque: false,
    link: null,
    imagem: null,
  },
  {
    id: 'lunna',
    nome: 'Projeto Lunna',
    icone: GraduationCap,
    problema:
      'Desenvolvimento de um aplicativo de alta performance focado na saúde e bem-estar para controle de rotinas e acompanhamento médico.',
    arquitetura:
      'Desenvolvido inteiramente em React Native no front-end móvel, integrado a uma API REST com isolamento de escopo no back-end. Defendido com nota máxima como Trabalho de Conclusão de Curso.',
    pilha: ['React Native', 'REST API', 'Saúde'],
    categoria: 'Projeto Acadêmico',
    destaque: false,
    link: null,
    imagem: null,
  },
  // ─── Novo card: Convites Digitais & Portais de Casamento ─────────────────
  {
    id: 'casamento',
    nome: 'Convites Digitais Interativos & Portais de Casamento',
    subtitulo: 'Experiências imersivas e inesquecíveis para o seu grande dia.',
    icone: Heart,
    problema:
      'Casais e famílias buscam uma experiência digital sofisticada e personalizada para comunicar seus eventos com elegância, substituindo convites físicos por plataformas imersivas que reflitam a identidade do casal.',
    arquitetura:
      'Desenvolvimento de plataformas web exclusivas para casamentos e eventos de luxo. Design moderno e minimalista com foco na jornada do usuário (UX). O projeto conta com animações fluidas cinematográficas, lista de presentes integrada, confirmação de presença (RSVP) automatizada e otimização de SEO/Open Graph para um link preview perfeito no WhatsApp.',
    pilha: ['Vue 3', 'Tailwind CSS', 'GSAP', 'Integração de APIs'],
    categoria: 'Alta-Costura Digital',
    destaque: true,
    link: 'https://samilly-e-hallerrandro.vercel.app/',
    imagem: '/projeto-casamento.jpg',
    isCasamento: true,
  },
]
</script>

<template>
  <section id="projetos" class="relative py-20 md:py-32 lg:py-40 px-4 md:px-12 lg:px-16 scroll-mt-20">
    <div class="max-w-7xl mx-auto">

      <!-- ─── Cabeçalho da Seção ───────────────────────────────────────────── -->
      <div class="mb-12 md:mb-20 lg:mb-28 flex flex-col md:flex-row md:items-end justify-between gap-6 md:gap-8">
        <div class="max-w-2xl">
          <span class="projeto-label gs-hidden font-mono text-xs font-medium tracking-[0.2em] uppercase text-magenta block mb-4 md:mb-6">
            § Projetos
          </span>
          <h2 class="projeto-title gs-hidden text-3xl sm:text-4xl md:text-5xl lg:text-7xl font-black tracking-brutal leading-[0.9] text-(--color-text-pure)">
            Sistemas em
            <span class="text-transparent bg-clip-text bg-linear-to-r from-ultraviolet to-magenta">Produção.</span>
          </h2>
        </div>
        <p class="projeto-desc gs-hidden text-(--color-text-muted) max-w-sm leading-relaxed font-medium text-sm md:text-base">
          Ferramentas que resolvem gargalos logísticos industriais com métricas mensuráveis de economia.
        </p>
      </div>

      <!-- ─── Grid de Projetos ──────────────────────────────────────────────── -->
      <div class="grid grid-cols-1 lg:grid-cols-12 gap-4 md:gap-6">

        <!-- ─── Cards de Projetos Padrão (não-casamento) ──────────────────── -->
        <template v-for="(projeto, index) in projetos" :key="projeto.id">

          <!-- Card de Casamento com identidade visual diferenciada -->
          <article
            v-if="projeto.isCasamento"
            class="projeto-card gs-hidden group relative lg:col-span-12
                   flex flex-col md:flex-row overflow-hidden rounded-3xl
                   bg-(--color-bg-surface)/40 backdrop-blur-2xl
                   border border-(--color-border) hover:border-magenta/40
                   transform-gpu will-change-transform
                   transition-all duration-500 ease-[cubic-bezier(0.25,1,0.5,1)]
                   hover:-translate-y-1 hover:shadow-[0_15px_50px_rgba(255,0,127,0.18)]
                   focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-magenta
                   active:scale-[0.99]"
          >
            <!-- Borda de refração de luz no topo — magenta para o casamento -->
            <div class="absolute top-0 left-0 right-0 h-px bg-linear-to-r from-transparent via-magenta/40 to-transparent rounded-t-3xl pointer-events-none" />

            <!-- Glow hover interno -->
            <div class="absolute inset-0 rounded-3xl bg-linear-to-br from-magenta/5 via-transparent to-ultraviolet/5 opacity-0 group-hover:opacity-100 transition-opacity duration-500 pointer-events-none" />

            <!-- Coluna da Imagem -->
            <div class="relative md:w-2/5 lg:w-2/5 min-h-[220px] md:min-h-auto overflow-hidden flex-shrink-0">
              <img
                :src="projeto.imagem"
                alt="Convite Digital Interativo — Portal de Casamento"
                class="w-full h-full object-cover transition-transform duration-700 group-hover:scale-105"
                loading="lazy"
              />
              <!-- Sobreposição de gradiente sobre a imagem -->
              <div class="absolute inset-0 bg-linear-to-r from-transparent to-(--color-bg-surface)/60 md:to-(--color-bg-surface)/80 pointer-events-none" />
              <!-- Badge de categoria sobre a imagem -->
              <span class="absolute top-4 left-4 px-3 py-1 font-mono text-[9px] tracking-widest uppercase
                           bg-magenta/90 text-white rounded-full shadow-lg backdrop-blur-sm">
                {{ projeto.categoria }}
              </span>
            </div>

            <!-- Coluna do Conteúdo -->
            <div class="flex flex-col justify-between p-6 md:p-8 lg:p-10 flex-1 relative z-10">

              <!-- Cabeçalho do card -->
              <div class="flex items-start justify-between mb-4 md:mb-6">
                <div class="flex items-center gap-3">
                  <div class="w-10 md:w-12 h-10 md:h-12 flex items-center justify-center rounded-xl
                              bg-magenta/10 text-magenta border border-magenta/20
                              group-hover:rotate-6 transition-all duration-500 ease-[cubic-bezier(0.34,1.56,0.64,1)]">
                    <component :is="projeto.icone" class="w-4 md:w-5 h-4 md:h-5" />
                  </div>
                </div>
                <span class="font-mono text-[10px] tracking-[0.2em] uppercase text-(--color-text-muted)/50 mt-2">
                  § {{ String(projetos.indexOf(projeto) + 1).padStart(2, '0') }}
                </span>
              </div>

              <!-- Título e Subtítulo -->
              <div class="mb-4 md:mb-6">
                <h3 class="text-xl md:text-2xl lg:text-3xl font-bold tracking-tight text-(--color-text-pure) mb-2">
                  {{ projeto.nome }}
                </h3>
                <p v-if="projeto.subtitulo" class="text-sm md:text-base text-magenta font-medium italic">
                  {{ projeto.subtitulo }}
                </p>
              </div>

              <!-- Descrição / Arquitetura -->
              <div class="flex flex-col gap-4 md:gap-5 mb-6 md:mb-8 flex-1">
                <p class="text-(--color-text-muted) leading-relaxed text-xs md:text-sm">
                  {{ projeto.arquitetura }}
                </p>
              </div>

              <!-- Rodapé: Tags + Botão -->
              <div class="flex flex-col gap-4 md:gap-5">
                <!-- Tags -->
                <div class="flex flex-wrap gap-2 pt-4 border-t border-(--color-border)">
                  <span
                    v-for="tech in projeto.pilha"
                    :key="tech"
                    class="px-2.5 md:px-3 py-1 md:py-1.5 font-mono text-[9px] md:text-[10px] font-medium tracking-wider
                           bg-(--color-bg-main)/60 text-(--color-text-muted)
                           border border-(--color-border)
                           rounded-full"
                  >
                    {{ tech }}
                  </span>
                </div>

                <!-- Botão Ver Projeto ao Vivo -->
                <a
                  :href="projeto.link"
                  target="_blank"
                  rel="noopener noreferrer"
                  class="inline-flex items-center gap-2 self-start
                         px-5 md:px-6 py-2.5 md:py-3 rounded-full
                         bg-magenta text-white font-semibold text-xs md:text-sm
                         shadow-[0_0_20px_rgba(255,0,127,0.3)]
                         hover:shadow-[0_0_30px_rgba(255,0,127,0.5)]
                         hover:scale-105 active:scale-95
                         focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-magenta
                         transform-gpu transition-all duration-300 ease-[cubic-bezier(0.25,1,0.5,1)]"
                  aria-label="Ver Projeto Ao Vivo — Convites Digitais"
                >
                  <Globe class="w-3.5 h-3.5" />
                  Ver Projeto Ao Vivo
                  <ExternalLink class="w-3 h-3 opacity-70" />
                </a>
              </div>

            </div>
          </article>

          <!-- Cards de projetos industriais/padrão -->
          <article
            v-else
            :class="[
              'projeto-card gs-hidden group relative flex flex-col p-6 md:p-8 lg:p-10',
              projeto.destaque ? 'lg:col-span-7' : 'lg:col-span-5',
              'bg-(--color-bg-surface)/40 backdrop-blur-2xl',
              'border border-(--color-border) hover:border-ultraviolet/40',
              'rounded-2xl',
              'hover:-translate-y-1',
              'active:scale-[0.99]',
              'focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-ultraviolet',
              'transform-gpu will-change-transform transition-all duration-500 ease-[cubic-bezier(0.25,1,0.5,1)]',
              'hover:shadow-[0_15px_40px_rgba(112,0,255,0.15)]',
            ]"
            tabindex="0"
          >
            <!-- Borda de refração de vidro no topo -->
            <div class="absolute top-0 left-0 right-0 h-px bg-linear-to-r from-transparent via-ultraviolet/30 to-transparent rounded-t-2xl pointer-events-none" />

            <!-- Glow hover interno -->
            <div class="absolute inset-0 rounded-2xl bg-linear-to-b from-ultraviolet/5 to-transparent opacity-0 group-hover:opacity-100 transition-opacity duration-500 pointer-events-none" />

            <!-- Cabeçalho do card -->
            <div class="flex items-start justify-between mb-6 md:mb-8 relative z-10">
              <div class="flex items-center gap-3">
                <div class="w-10 md:w-12 h-10 md:h-12 flex items-center justify-center rounded-xl
                            bg-ultraviolet/10 text-ultraviolet border border-ultraviolet/15
                            group-hover:text-magenta group-hover:border-magenta/30
                            group-hover:rotate-6 transition-all duration-500 ease-[cubic-bezier(0.34,1.56,0.64,1)]">
                  <component :is="projeto.icone" class="w-4 md:w-5 h-4 md:h-5" />
                </div>
                <span v-if="projeto.categoria" class="px-2.5 py-1 font-mono text-[8px] tracking-wider uppercase bg-magenta/10 text-magenta rounded border border-magenta/25">
                  {{ projeto.categoria }}
                </span>
              </div>
              <span class="font-mono text-[10px] tracking-[0.2em] uppercase text-(--color-text-muted)/50 mt-2">
                § {{ String(index + 1).padStart(2, '0') }}
              </span>
            </div>

            <h3 class="relative z-10 text-xl md:text-2xl lg:text-3xl font-bold tracking-tight text-(--color-text-pure) mb-4 md:mb-6">
              {{ projeto.nome }}
            </h3>

            <!-- Conteúdo: Problema e Solução -->
            <div class="relative z-10 flex flex-col gap-4 md:gap-6 mb-8 md:mb-10 flex-1">
              <div>
                <h4 class="font-mono text-[10px] font-semibold uppercase tracking-[0.2em] text-magenta mb-2">
                  Problema
                </h4>
                <p class="text-(--color-text-muted) leading-relaxed text-xs md:text-sm">
                  {{ projeto.problema }}
                </p>
              </div>
              <div v-if="projeto.destaque">
                <h4 class="font-mono text-[10px] font-semibold uppercase tracking-[0.2em] text-magenta mb-2">
                  Solução
                </h4>
                <p class="text-(--color-text-muted) leading-relaxed text-xs md:text-sm">
                  {{ projeto.arquitetura }}
                </p>
              </div>
            </div>

            <!-- Tags da pilha tecnológica -->
            <div class="relative z-10 flex flex-wrap gap-2 mt-auto pt-4 md:pt-6 border-t border-(--color-border)">
              <span
                v-for="tech in projeto.pilha"
                :key="tech"
                class="px-2.5 md:px-3 py-1 md:py-1.5 font-mono text-[9px] md:text-[10px] font-medium tracking-wider
                       bg-(--color-bg-main)/60 text-(--color-text-muted)
                       border border-(--color-border)
                       rounded-full"
              >
                {{ tech }}
              </span>
            </div>
          </article>

        </template>
      </div>
    </div>
  </section>
</template>
