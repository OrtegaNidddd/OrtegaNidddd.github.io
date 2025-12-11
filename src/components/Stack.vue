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
                <div class="w-10 h-10 rounded-lg bg-gradient-to-br from-purple-500/20 to-blue-500/20 flex items-center justify-center border border-purple-500/30">
                    <svg class="w-5 h-5 text-purple-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 20l4-16m4 4l4 4-4 4M6 16l-4-4 4-4"/>
                    </svg>
                </div>
                <h3 class="text-lg font-bold tracking-wide">
                    Stack Tecnológico
                </h3>
            </div>
            
            <div class="grid grid-cols-2 gap-3">
                <div
                    v-for="tech in technologies" 
                    :key="tech.name"
                    @mouseenter="hoveredTech = tech.name"
                    @mouseleave="hoveredTech = null"
                    class="group relative"
                >
                    <!-- Badge  -->
                    <div 
                        :class="[
                            tech.color,
                            'relative overflow-hidden rounded-xl px-4 py-3.5 text-sm font-semibold text-center border-2 transition-all duration-300 cursor-pointer backdrop-blur-sm'
                        ]"
                        class="transform hover:scale-105 hover:shadow-lg"
                    >
                        <!-- Brillo al hacer hover -->
                        <div class="absolute inset-0 bg-gradient-to-r from-transparent via-white/10 to-transparent translate-x-[-100%] group-hover:translate-x-[100%] transition-transform duration-700"></div>
                    
                        <!-- Contenido -->
                        <div class="relative flex items-center justify-center gap-2">
                            <span>{{ tech.name }}</span>
                        </div>

                        <!-- Barra de nivel -->
                        <div class="absolute bottom-0 left-0 right-0 h-1 bg-gray-800/30 overflow-hidden">
                            <div 
                                :class="tech.levelColor"
                                :style="{ width: tech.level + '%' }"
                                class="h-full transition-all duration-500 group-hover:animate-pulse"
                            ></div>
                        </div>
                    </div>
                </div>
            </div>

            <Separador />

            <!-- Estadísticas -->
            <div class="pt-4 grid grid-cols-3 gap-4 text-center">
                <div class="space-y-1">
                    <div class="text-2xl font-bold">{{ technologies.length }}</div>
                    <div class="text-xs">Tecnologías</div>
                </div>
                <div class="space-y-1">
                    <div class="text-2xl font-bold bg-gradient-to-r from-purple-600 to-indigo-500 bg-clip-text text-transparent">
                        {{ advancedCount }}
                    </div>
                    <div class="text-xs">Avanzadas</div>
                </div>
                <div class="space-y-1">
                    <div class="text-2xl font-bold">{{ averageLevel }}%</div>
                    <div class="text-xs text-gray-400">Nivel Promedio</div>
                </div>
            </div>
        </div>
        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                hoveredTech: null,
                technologies: [
                    { 
                        name: 'Vue',
                        level: 60,
                        levelColor: 'bg-gradient-to-r from-emerald-400 to-emerald-500',
                        color: 'bg-gradient-to-br from-emerald-400/10 to-emerald-500/20 border-emerald-400/50 hover:border-emerald-400 hover:from-emerald-400/20 hover:to-emerald-500/30'
                    },
                    { 
                        name: 'Laravel',
                        level: 75,
                        levelColor: 'bg-gradient-to-r from-red-400 to-red-500',
                        color: 'bg-gradient-to-br from-red-400/10 to-red-500/20 border-red-400/50 hover:border-red-400 hover:from-red-400/20 hover:to-red-500/30'
                    },
                    { 
                        name: 'Tailwind',
                        level: 90,
                        levelColor: 'bg-gradient-to-r from-cyan-400 to-cyan-500',
                        color: 'bg-gradient-to-br from-cyan-400/10 to-cyan-500/20 border-cyan-400/50 hover:border-cyan-400 hover:from-cyan-400/20 hover:to-cyan-500/30'
                    },
                    { 
                        name: 'JavaScript',
                        level: 70,
                        levelColor: 'bg-gradient-to-r from-yellow-400 to-yellow-500',
                        color: 'bg-gradient-to-br from-yellow-400/10 to-yellow-500/20 border-yellow-500/50 hover:border-yellow-400 hover:from-yellow-400/20 hover:to-yellow-500/30'
                    },
                    { 
                        name: 'Node.js',
                        level: 50,
                        levelColor: 'bg-gradient-to-r from-green-400 to-green-500',
                        color: 'bg-gradient-to-br from-green-400/10 to-green-500/20 border-green-400/50 hover:border-green-400 hover:from-green-400/20 hover:to-green-500/30'
                    },
                    { 
                        name: 'MySQL',
                        level: 85,
                        levelColor: 'bg-gradient-to-r from-blue-400 to-blue-500',
                        color: 'bg-gradient-to-br from-blue-400/10 to-blue-500/20 border-blue-400/50 hover:border-blue-400 hover:from-blue-400/20 hover:to-blue-500/30'
                    },
                    { 
                        name: 'PostgreSQL',
                        level: 70,
                        levelColor: 'bg-gradient-to-r from-indigo-400 to-indigo-500',
                        color: 'bg-gradient-to-br from-indigo-400/10 to-indigo-500/20 border-indigo-400/50 hover:border-indigo-400 hover:from-indigo-400/20 hover:to-indigo-500/30'
                    },
                    { 
                        name: 'Postman',
                        level: 80,
                        levelColor: 'bg-gradient-to-r from-amber-400 to-amber-500',
                        color: 'bg-gradient-to-br from-amber-400/10 to-amber-500/20 border-amber-500/50 hover:border-amber-400 hover:from-amber-400/20 hover:to-amber-500/30'
                    }
                ]
            };
        },
        computed: {
            advancedCount() {
                return this.technologies.filter(tech => tech.level >= 85).length;
            },
            averageLevel() {
                const sum = this.technologies.reduce((acc, tech) => acc + tech.level, 0);
                return Math.round(sum / this.technologies.length);
            }
        }
    };
</script>