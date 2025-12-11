<script setup>
    import Aptitudes from './Aptitudes.vue' 
    import Separador from './Separador.vue'
    import Stack from './Stack.vue'
</script>

<template>

    <section id="aboutMe" class="relative" >
        <div class="max-w-6xl mx-auto px-6 lg:px-10 py-10">
            <!-- Título -->
            <h2 class="text-center text-3xl lg:text-4xl font-extrabold tracking-tight">
                Sobre mí
            </h2>
            <div class="mx-auto mt-3 h-1 w-24 rounded-full bg-gradient-to-r from-fuchsia-500 to-sky-500"></div>

            <!-- Contenido -->
            <div class="mt-10 flex flex-col gap-8" >
                <!-- Texto -->
                <div class="md:col-span-3">
                    <p class="text-base lg:text-lg leading-8">
                        Soy estudiante de Ingeniería de Software, actualmente aprendiendo
                        <span class="font-semibold">Laravel, Node.js, Express y Vue</span>.
                        Me interesa la ciberseguridad y me caracterizo por un trabajo ágil y
                        eficiente sin sacrificar la calidad. Soy responsable, comprometido y
                        siempre dispuesto a colaborar, apasionado por lo que hago y dando siempre el 100%.
                    </p>
                    <Separador />
                </div>


            <div class="flex flex-col md:flex-row gap-8 md:gap-12 justify-center items-center">
                        <Aptitudes />
                    
                        <Stack />
                </div>
            </div>
        </div>
    </section>

</template>