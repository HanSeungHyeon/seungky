<template>
  <div id="layout">
    <NavBar />
    <main>
      <HeroSection />
      <AboutSection />
      <ExperienceSection />
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
import ExperienceSection from './components/ExperienceSection.vue'
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

section + section {
  border-top: 1px solid var(--border);
}
</style>
