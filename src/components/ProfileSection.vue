<script setup>

defineProps({
    linkProfile: String,
})

</script>

<template>

    <section class="mt-26 w-full px-6 lg:px-16 py-10 " style="background-color: var(--dark-color);">
        <div class="max-w-6xl mx-auto">
            <!-- Nombre -->
            <h1
            class="mb-6 py-2 text-3xl text-center lg:text-left lg:text-5xl font-extrabold text-transparent bg-clip-text bg-gradient-to-r from-sky-500 to-pink-500">
            Nick Alejandro Ortega Mendez
            </h1>

            <!-- Contenido -->
            <div class="flex flex-col md:flex-row items-center md:items-start justify-between gap-8">
                <!-- Texto -->
                <div class="w-full md:w-3/5">
                    <span class="block text-2xl lg:text-3xl font-bold">
                    Fullstack Developer Jr.
                    </span>
                    <p class="mt-4 text-base lg:text-lg leading-relaxed">
                    Desarrollador fullstack en formación con enfoque en la construcción de soluciones web modernas, escalables y bien estructuradas. Apasionado por el aprendizaje continuo y la optimización de procesos mediante tecnología.
                    </p>
                </div>

                <!-- Avatar -->
                <div class="w-full md:w-auto flex justify-center md:justify-end">
                    <a :href="linkProfile" target="_blank" rel="noopener noreferrer" aria-label="Ver perfil">
                        <div class="relative rounded-full p-[3px] bg-gradient-to-r from-sky-500 to-pink-500">
                        <img
                            src="../assets/profile.jpg"
                            alt="Foto de perfil de Nick Alejandro Ortega Mendez"
                            class="block w-40 h-40 md:w-56 md:h-56 rounded-full object-cover ring-1 ring-black/10"
                        />
                        </div>
                    </a>
                </div>
            </div>

        </div>
    </section>


</template>