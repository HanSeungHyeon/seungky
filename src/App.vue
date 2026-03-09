<template>
  <div id="layout">
    <NavBar />
    <main>
      <HeroSection />
      <AboutSection />
      <ProjectsSection />
      <ContactSection />
    </main>
    <FooterBar />
  </div>
</template>

<script setup>
import NavBar          from './components/NavBar.vue'
import HeroSection     from './components/HeroSection.vue'
import AboutSection    from './components/AboutSection.vue'
import ProjectsSection from './components/ProjectsSection.vue'
import ContactSection  from './components/ContactSection.vue'
import FooterBar       from './components/FooterBar.vue'
</script>

<style>
#layout {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
}
main { flex: 1; }
</style>
