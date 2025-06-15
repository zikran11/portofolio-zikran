<script setup lang="ts">
import { onMounted } from 'vue'
import Navigation from './components/Navigation.vue'
import Hero from './components/Hero.vue'
import About from './components/About.vue'
import Skills from './components/Skills.vue'
import Projects from './components/Projects.vue'
import Contact from './components/Contact.vue'
import Background from './components/Background.vue'
import { initSmoothScroll } from './utils/scroll'

onMounted(() => {
  initSmoothScroll()
})
</script>

<template>
  <div id="app">
    <Background />
    <Navigation />
    <Hero />
    <About />
    <Skills />
    <Projects />
    <Contact />
  </div>
</template>

<style scoped>
#app {
  position: relative;
}
</style>