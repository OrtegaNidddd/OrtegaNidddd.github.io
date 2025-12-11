<script setup>
  import NavBar from './components/NavBar.vue'
  import ProfileSection from './components/ProfileSection.vue'
  import AboutMe from './components/AboutMe.vue'
  import Separador from './components/Separador.vue'
  import Projects from './components/Projects.vue'
  import Contact from './components/Contact.vue'
</script>


<template>


  <NavBar msg="" linkProfile="https://github.com/OrtegaNidddd" />

  <ProfileSection msg="" linkProfile="https://github.com/OrtegaNidddd"/>

  <Separador />

  <AboutMe />

  <Projects/>

  <Contact linkGithub="https://github.com/OrtegaNidddd" linkInstagram="https://www.instagram.com/nick._.ortega/"/>

</template>




<style scoped>

</style>