<script setup>
import { ref } from 'vue';
import ThemeButton from './ThemeButton.vue';
import logo from '../assets/icon.png';

defineProps({
  msg: String,
  linkProfile: String,
})

const isMenuOpen = ref(false);

const toggleMenu = () => {
  isMenuOpen.value = !isMenuOpen.value;
}

const closeMenu = () => {
  isMenuOpen.value = false;
}
</script>

<template>
  <nav class="p-1 py-4 lg:p-4 fixed top-0 left-0 w-full z-40" id="#" style="background-color: var(--dark-color);">
    
    <div class="hidden lg:flex justify-center items-center">
      <a
        :href="linkProfile"
        class="hover:text-sky-400 duration-200 ease-in-out w-2/6 flex items-center justify-center gap-3"
        target="_blank"
      >
        <img :src="logo" alt="Logotipo OrtegaNidddd" class="h-14 w-14 rounded-full" />
        <div class="text-lg font-semibold cursor-pointer">OrtegaNidddd</div>
      </a>
      <div class="flex text-lg w-4/6 overflow-hidden justify-center items-center">
        <a href="#" class="px-3 hover:text-sky-500 duration-200 ease-in-out">Inicio</a>
        <a href="#aboutMe" class="px-3 hover:text-sky-500 duration-200 ease-in-out">Sobre mí</a>
        <a href="#projects" class="px-3 hover:text-sky-500 duration-200 ease-in-out">Proyectos</a>
        <a href="#contacto" class="px-3 hover:text-sky-500 duration-200 ease-in-out">Contacto</a>
      </div>
      <div class="w-2/6 flex justify-end pr-4">
        <ThemeButton />
      </div>
    </div>

    <div class="lg:hidden flex justify-between items-center px-4">
      <a
        :href="linkProfile"
        class="hover:text-sky-400 duration-200 ease-in-out flex items-center gap-2"
        target="_blank"
      >
        <img :src="logo" alt="Logotipo OrtegaNidddd" class="h-12 w-12 rounded-full" />
        <div class="text-sm font-semibold">OrtegaNidddd</div>
      </a>
      
      <div class="flex items-center gap-4">
        <ThemeButton />
        <!-- Hamburger Button -->
        <button @click="toggleMenu" class="focus:outline-none" aria-label="Toggle menu">
          <div class="w-6 h-5 flex flex-col justify-between">
            <span 
              class="block h-0.5 w-full bg-current transform transition duration-300 ease-in-out"
              :class="isMenuOpen ? 'rotate-45 translate-y-2' : ''"
            ></span>
            <span 
              class="block h-0.5 w-full bg-current transition duration-300 ease-in-out"
              :class="isMenuOpen ? 'opacity-0' : 'opacity-100'"
            ></span>
            <span 
              class="block h-0.5 w-full bg-current transform transition duration-300 ease-in-out"
              :class="isMenuOpen ? '-rotate-45 -translate-y-2' : ''"
            ></span>
          </div>
        </button>
      </div>
    </div>

    <!-- Mobile Menu -->
    <transition
      enter-active-class="transition ease-out duration-200"
      enter-from-class="opacity-0 -translate-y-4"
      enter-to-class="opacity-100 translate-y-0"
      leave-active-class="transition ease-in duration-150"
      leave-from-class="opacity-100 translate-y-0"
      leave-to-class="opacity-0 -translate-y-4"
    >
      <div 
        v-if="isMenuOpen" 
        class="lg:hidden absolute top-full left-0 w-full shadow-lg"
        style="background-color: var(--dark-color);"
      >
        <div class="flex flex-col py-4 px-6 space-y-3">
          <a href="#" @click="closeMenu" class="py-2 hover:text-sky-500 duration-200 ease-in-out">Inicio</a>
          <a href="#aboutMe" @click="closeMenu" class="py-2 hover:text-sky-500 duration-200 ease-in-out">Sobre mí</a>
          <a href="#projects" @click="closeMenu" class="py-2 hover:text-sky-500 duration-200 ease-in-out">Proyectos</a>
          <a href="#contacto" @click="closeMenu" class="py-2 hover:text-sky-500 duration-200 ease-in-out">Contacto</a>
        </div>
      </div>
    </transition>
  </nav>
</template>
