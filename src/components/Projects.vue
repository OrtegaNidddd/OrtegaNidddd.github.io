<script setup>
import Card from './ProjectCard.vue'

const categories = [
  {
    key: 'sold',
    label: 'Soluciones implementadas',
    description: 'Proyectos que ya estan en produccion generando resultados.',
    dot: 'bg-amber-400'
  },
  {
    key: 'personal',
    label: 'Proyectos personales',
    description: 'Espacio de experimentacion constante y mejoras continuas.',
    dot: 'bg-indigo-400'
  },
  {
    key: 'academic',
    label: 'Proyectos academicos',
    description: 'Trabajo colaborativo guiado por investigacion y practica.',
    dot: 'bg-emerald-400'
  }
]

const projects = [
  {
    title: 'Seguros con Maritza',
    description:
      'Landing page enfocada en captar leads para una asesora de seguros con formularios inteligentes, bloques educativos y automatizacion hacia WhatsApp Business.',
    technologies: ['Next.js', 'TypeScript', 'Tailwind'],
    linkDemo: 'https://segurosconmaritza.com',
    linkRepo: '',
    status: 'Implementado',
    scope: 'Landing para una asesora de seguros, orientada a generar contactos y solicitudes.',
    categories: ['sold']
  },
  {
    title: 'AURUM',
    description:
      'Plataforma web que digitaliza el proceso del taller de joyeria artesanal: pedidos, catalogos, gestion de insumos y flujo creativo en un mismo lugar.',
    technologies: ['Vue', 'Laravel', 'Tailwind'],
    linkDemo: 'https://github.com/OrtegaNidddd/jewelry_workshop',
    linkRepo: 'https://github.com/OrtegaNidddd/jewelry_workshop',
    status: 'En progreso',
    scope: 'Producto fullstack para taller joyero artesanal',
    categories: ['personal', 'academic']
  },
  {
    title: 'Gestor de imagenes',
    description:
      'Suite de utilidades para convertir, redimensionar y comprimir imagenes con perfiles preconfigurados para contenido institucional.',
    technologies: ['Laravel', 'Tailwind', 'JavaScript'],
    linkDemo: 'https://forestgreen-partridge-240286.hostingersite.com/',
    linkRepo: 'https://github.com/OrtegaNidddd/conversor-imagenes',
    status: 'Completado',
    scope: 'Herramienta personal para acelerar despliegues de contenido',
    categories: ['personal']
  },
  {
    title: 'Generador de codigos QR',
    description:
      'Aplicacion web que crea codigos QR personalizables con vista previa en tiempo real, descarga inmediata y controles de contraste.',
    technologies: ['Laravel', 'Tailwind'],
    linkDemo: 'https://darkorchid-hedgehog-545748.hostingersite.com/',
    linkRepo: 'https://github.com/OrtegaNidddd/conversor-imagenes',
    status: 'Completado',
    scope: 'Microservicio para campanas de marketing y material impreso',
    categories: ['personal']
  }
]

const getProjectsByCategory = (key) =>
  projects.filter((project) => project.categories.includes(key))

const sectionStyles = {
  background: 'var(--section-surface)',
  color: 'var(--text-primary)'
}

const mutedTextStyle = {
  color: 'var(--text-muted)'
}

const panelStyles = {
  background: 'var(--panel-surface)',
  borderColor: 'var(--panel-border)',
  boxShadow: 'var(--panel-shadow)'
}
</script>

<template>
  <section
    id="projects"
    class="py-16 px-4 sm:px-6 lg:px-8 transition-colors duration-300"
    :style="sectionStyles"
  >
    <div class="max-w-6xl mx-auto space-y-12">
      <header class="text-center space-y-4">
        <p class="text-xs uppercase tracking-[0.35em] text-indigo-400">
          Roadmap en accion
        </p>
        <h2 class="text-3xl lg:text-4xl font-extrabold tracking-tight">
          Proyectos que representan mi forma de trabajar
        </h2>
        <p class="text-base max-w-3xl mx-auto" :style="mutedTextStyle">
          Dividi la seleccion por contexto para mostrar como adapto procesos, herramientas y
          comunicaciones segun cada reto.
        </p>
      </header>

      <template v-for="category in categories" :key="category.key">
        <div
          v-if="getProjectsByCategory(category.key).length"
          class="rounded-3xl border p-6 md:p-10 space-y-6 backdrop-blur-xl transition-colors duration-300"
          :style="panelStyles"
        >
          <div class="flex flex-col gap-2">
            <div class="flex items-center gap-3">
              <span :class="category.dot" class="h-2.5 w-2.5 rounded-full"></span>
              <p class="text-sm uppercase tracking-[0.25em]" :style="mutedTextStyle">
                {{ category.label }}
              </p>
            </div>
            <p class="text-lg font-semibold">
              {{ category.description }}
            </p>
          </div>

          <div class="grid grid-cols-1 lg:grid-cols-2 gap-6">
            <Card
              v-for="project in getProjectsByCategory(category.key)"
              :key="project.title + category.key"
              :title="project.title"
              :description="project.description"
              :technologies="project.technologies"
              :linkDemo="project.linkDemo"
              :linkRepo="project.linkRepo"
              :status="project.status"
              :scope="project.scope"
            />
          </div>
        </div>
      </template>
    </div>
  </section>
</template>
