<script setup>
  import Separador from './Separador.vue';
</script>

<template>
  <div class="md:col-span-2 w-full lg:w-2/4">
    <div class="relative rounded-2xl border backdrop-blur-sm p-6 shadow-xl shadow-black/30 overflow-hidden" 
         style="border-color: var(--dark-color);">
      
      <!-- Efecto de brillo de fondo -->
      <div class="absolute inset-0 bg-gradient-to-br from-transparent via-white/5 to-transparent opacity-0 hover:opacity-100 transition-opacity duration-500 pointer-events-none"></div>
      
      <div class="relative z-10">
        <div class="flex items-center gap-3 mb-6">
          <div class="w-10 h-10 rounded-lg bg-gradient-to-br from-indigo-500/20 to-purple-500/20 flex items-center justify-center border border-indigo-500/30">
            <svg class="w-5 h-5 text-indigo-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9.663 17h4.673M12 3v1m6.364 1.636l-.707.707M21 12h-1M4 12H3m3.343-5.657l-.707-.707m2.828 9.9a5 5 0 117.072 0l-.548.547A3.374 3.374 0 0014 18.469V19a2 2 0 11-4 0v-.531c0-.895-.356-1.754-.988-2.386l-.548-.547z"/>
            </svg>
          </div>
          <h3 class="text-lg font-bold tracking-wide">
            Aptitudes
          </h3>
        </div>
        
        <div class="grid grid-cols-2 gap-3">
          <div
            v-for="(aptitud, index) in aptitudes" 
            :key="index"
            @mouseenter="hoveredAptitud = index"
            @mouseleave="hoveredAptitud = null"
            class="group relative"
          >
            <!-- Badge -->
            <div 
              :class="[
                aptitud.gradient,
                'relative overflow-hidden rounded-xl px-4 py-3.5 text-sm font-semibold text-center border-2 transition-all duration-300 cursor-pointer backdrop-blur-sm'
              ]"
              class="transform hover:scale-105 hover:shadow-xl"
            >
              <!-- Efecto de brillo animado -->
              <div class="absolute inset-0 bg-gradient-to-r from-transparent via-white/20 to-transparent translate-x-[-100%] group-hover:translate-x-[100%] transition-transform duration-700"></div>
              
              <!-- Icono y texto -->
              <div class="relative flex items-center justify-center gap-2">
                <component :is="aptitud.icon" class="w-4 h-4 opacity-0 group-hover:opacity-100 transition-opacity duration-200" />
                <span class="">{{ aptitud.name }}</span>
              </div>


            </div>
          </div>
        </div>

        <Separador />

        <!-- Estadísticas -->
        <div class="pt-4 flex items-center justify-between text-sm">
          <span >Total de aptitudes</span>
          <span class="font-bol bg-gradient-to-r from-indigo-500/20 to-purple-500/20 px-3 py-1 rounded-full border border-indigo-500/30">
            {{ aptitudes.length }}
          </span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      hoveredAptitud: null,
      aptitudes: [
        { 
          name: 'Visión',
          icon: 'IconEye',
          gradient: 'bg-gradient-to-br from-blue-400/10 to-cyan-500/20 border-blue-400/50 hover:border-blue-400 hover:from-blue-400/20 hover:to-cyan-500/30'
        },
        { 
          name: 'Disciplina',
          icon: 'IconTarget',
          gradient: 'bg-gradient-to-br from-purple-400/10 to-pink-500/20 border-purple-400/50 hover:border-purple-400 hover:from-purple-400/20 hover:to-pink-500/30'
        },
        { 
          name: 'Efectividad',
          icon: 'IconCheckCircle',
          gradient: 'bg-gradient-to-br from-green-400/10 to-emerald-500/20 border-green-400/50 hover:border-green-400 hover:from-green-400/20 hover:to-emerald-500/30'
        },
        { 
          name: 'Adaptabilidad',
          icon: 'IconRefresh',
          gradient: 'bg-gradient-to-br from-orange-400/10 to-amber-500/20 border-orange-400/50 hover:border-orange-400 hover:from-orange-400/20 hover:to-amber-500/30'
        },
        { 
          name: 'Trabajo en equipo',
          icon: 'IconUsers',
          gradient: 'bg-gradient-to-br from-indigo-400/10 to-blue-500/20 border-indigo-400/50 hover:border-indigo-400 hover:from-indigo-400/20 hover:to-blue-500/30'
        },
        { 
          name: 'Aprendizaje rápido',
          icon: 'IconBolt',
          gradient: 'bg-gradient-to-br from-yellow-400/10 to-orange-500/20 border-yellow-400/50 hover:border-yellow-400 hover:from-yellow-400/20 hover:to-orange-500/30'
        },
        { 
          name: 'Atención al detalle',
          icon: 'IconSearch',
          gradient: 'bg-gradient-to-br from-teal-400/10 to-cyan-500/20 border-teal-400/50 hover:border-teal-400 hover:from-teal-400/20 hover:to-cyan-500/30'
        },
        { 
          name: 'Resolución de problemas',
          icon: 'IconPuzzle',
          gradient: 'bg-gradient-to-br from-red-400/10 to-rose-500/20 border-red-400/50 hover:border-red-400 hover:from-red-400/20 hover:to-rose-500/30'
        }
      ]
    };
  },
  computed: {
    highlightedCount() {
      return this.aptitudes.filter(apt => apt.level >= 90).length;
    },
    averageLevel() {
      const sum = this.aptitudes.reduce((acc, apt) => acc + apt.level, 0);
      return Math.round(sum / this.aptitudes.length);
    }
  },
  components: {
    IconEye: {
      template: `
        <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z"/>
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M2.458 12C3.732 7.943 7.523 5 12 5c4.478 0 8.268 2.943 9.542 7-1.274 4.057-5.064 7-9.542 7-4.477 0-8.268-2.943-9.542-7z"/>
        </svg>
      `
    },
    IconTarget: {
      template: `
        <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 2C6.48 2 2 6.48 2 12s4.48 10 10 10 10-4.48 10-10S17.52 2 12 2zm0 18c-4.41 0-8-3.59-8-8s3.59-8 8-8 8 3.59 8 8-3.59 8-8 8zm0-14c-3.31 0-6 2.69-6 6s2.69 6 6 6 6-2.69 6-6-2.69-6-6-6zm0 10c-2.21 0-4-1.79-4-4s1.79-4 4-4 4 1.79 4 4-1.79 4-4 4z"/>
        </svg>
      `
    },
    IconCheckCircle: {
      template: `
        <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z"/>
        </svg>
      `
    },
    IconRefresh: {
      template: `
        <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 4v5h.582m15.356 2A8.001 8.001 0 004.582 9m0 0H9m11 11v-5h-.581m0 0a8.003 8.003 0 01-15.357-2m15.357 2H15"/>
        </svg>
      `
    },
    IconUsers: {
      template: `
        <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 4.354a4 4 0 110 5.292M15 21H3v-1a6 6 0 0112 0v1zm0 0h6v-1a6 6 0 00-9-5.197M13 7a4 4 0 11-8 0 4 4 0 018 0z"/>
        </svg>
      `
    },
    IconBolt: {
      template: `
        <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 10V3L4 14h7v7l9-11h-7z"/>
        </svg>
      `
    },
    IconSearch: {
      template: `
        <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"/>
        </svg>
      `
    },
    IconPuzzle: {
      template: `
        <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M11 4a2 2 0 114 0v1a1 1 0 001 1h3a1 1 0 011 1v3a1 1 0 01-1 1h-1a2 2 0 100 4h1a1 1 0 011 1v3a1 1 0 01-1 1h-3a1 1 0 01-1-1v-1a2 2 0 10-4 0v1a1 1 0 01-1 1H7a1 1 0 01-1-1v-3a1 1 0 00-1-1H4a2 2 0 110-4h1a1 1 0 001-1V7a1 1 0 011-1h3a1 1 0 001-1V4z"/>
        </svg>
      `
    }
  }
};
</script>