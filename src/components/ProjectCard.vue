<script setup>
import { computed } from 'vue'

const props = defineProps({
  title: String,
  description: String,
  technologies: {
    type: Array,
    default: () => []
  },
  linkDemo: {
    type: String,
    default: '#'
  },
  linkRepo: {
    type: String,
    default: '#'
  },
  status: {
    type: String,
    default: 'Completado'
  },
  scope: {
    type: String,
    default: ''
  }
})

const cardStyles = {
  background: 'var(--card-surface)',
  borderColor: 'var(--card-border)',
  boxShadow: 'var(--card-shadow)',
  color: 'var(--text-primary)'
}

const mutedTextStyle = {
  color: 'var(--text-muted)'
}

const secondaryButtonStyle = {
  borderColor: 'var(--secondary-btn-border)',
  color: 'var(--secondary-btn-text)'
}

const chipStyle = {
  color: 'var(--text-primary)'
}

const getTechColor = (tech) => {
  const colors = {
    React: 'bg-blue-500/15 border-blue-500/35',
    Vue: 'bg-emerald-500/15 border-emerald-500/35',
    TypeScript: 'bg-indigo-500/15 border-indigo-500/35',
    'Node.js': 'bg-green-500/15 border-green-500/35',
    Laravel: 'bg-red-500/15 border-red-500/35',
    Tailwind: 'bg-cyan-500/15 border-cyan-500/35',
    JavaScript: 'bg-yellow-500/15 border-yellow-500/35',
    Python: 'bg-blue-600/15 border-blue-600/35',
    'Next.js': 'bg-sky-500/15 border-sky-500/35',
    PHP: 'bg-purple-500/15 border-purple-500/35',
    WordPress: 'bg-slate-500/15 border-slate-500/35',
    Elementor: 'bg-fuchsia-500/15 border-fuchsia-500/35',
    GA4: 'bg-amber-500/15 border-amber-500/35'
  }

  return colors[tech] || 'bg-slate-200 border-slate-300'
}

const getStatusColor = (status) => {
  const colors = {
    Completado: 'bg-emerald-500/15 text-emerald-500 border border-emerald-400/30',
    'En progreso': 'bg-amber-400/20 text-amber-500 border border-amber-400/40',
    Implementado: 'bg-sky-400/20 text-sky-600 border border-sky-400/40'
  }

  return colors[status] || 'bg-slate-200 text-slate-700 border border-slate-300'
}

const hasRepo = computed(() => props.linkRepo && props.linkRepo !== '#')
</script>

<template>
  <article
    class="group flex h-full flex-col rounded-2xl border p-6 transition-all duration-300 hover:-translate-y-1"
    :style="cardStyles"
  >
    <div class="flex items-start justify-between gap-4 mb-6">
      <span :class="getStatusColor(status)" class="inline-flex px-3 py-1 text-xs text-center font-semibold rounded-full">
        {{ status }}
      </span>
      <span
        v-if="scope"
        class="text-[0.65rem] uppercase tracking-[0.35em] text-right"
        :style="mutedTextStyle"
      >
        {{ scope }}
      </span>
    </div>

    <div class="space-y-4 flex-1">
      <h3 class="text-2xl font-semibold">
        {{ title }}
      </h3>
      <p class="text-sm leading-relaxed" :style="mutedTextStyle">
        {{ description }}
      </p>
    </div>

    <div class="mt-6">
      <p class="text-xs uppercase tracking-[0.25em] mb-3" :style="mutedTextStyle">
        Tecnologias clave
      </p>
      <div class="flex flex-wrap gap-2">
        <span
          v-for="tech in technologies"
          :key="tech"
          :class="getTechColor(tech)"
          class="text-xs font-semibold px-3 py-1 rounded-full border"
          :style="chipStyle"
        >
          {{ tech }}
        </span>
      </div>
    </div>

    <div class="mt-8 flex flex-col sm:flex-row gap-3">
      <a
        :href="linkDemo"
        target="_blank"
        class="flex-1 inline-flex items-center justify-center gap-2 rounded-xl bg-indigo-500/90 px-4 py-2.5 text-sm font-semibold text-white transition-colors duration-200 hover:bg-indigo-400"
      >
        <svg class="w-4 h-4" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24">
          <path stroke-linecap="round" stroke-linejoin="round" d="M9 5l7 7-7 7" />
        </svg>
        Ver proyecto
      </a>
      <a
        v-if="hasRepo"
        :href="linkRepo"
        target="_blank"
        class="inline-flex items-center justify-center gap-2 rounded-xl border px-4 py-2.5 text-sm font-semibold transition-all duration-200"
        :style="secondaryButtonStyle"
      >
        <svg class="w-4 h-4" fill="currentColor" viewBox="0 0 24 24">
          <path
            d="M12 0C5.373 0 0 5.373 0 12c0 5.303 3.438 9.8 8.205 11.387.6.111.793-.261.793-.577v-2.234c-3.338.726-4.034-1.416-4.034-1.416-.546-1.387-1.332-1.756-1.332-1.756-1.089-.745.083-.729.083-.729 1.206.084 1.839 1.237 1.839 1.237 1.069 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.302 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.046.138 3.005.404 2.292-1.552 3.299-1.23 3.299-1.23.652 1.653.242 2.874.118 3.176.769.84 1.234 1.911 1.234 3.221 0 4.607-2.804 5.621-5.476 5.918.43.372.822 1.102.822 2.222v3.293c0 .319.192.693.801.576C20.565 21.796 24 17.299 24 12c0-6.627-5.373-12-12-12z"
          />
        </svg>
        Ver codigo
      </a>
    </div>
  </article>
</template>
