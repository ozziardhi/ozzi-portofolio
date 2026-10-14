<script setup>
import Navbar from './components/Navbar.vue'
import HeroSection from './components/HeroSection.vue'
import AboutSection from './components/AboutSection.vue'
import SkillsSection from './components/SkillsSection.vue'
import ExperienceSection from './components/ExperienceSection.vue'
import ProjectsSection from './components/ProjectsSection.vue'
import Footer from './components/Footer.vue'
</script>

<template>
  <!-- Tambahkan class retro-grid-bg di sini -->
  <div class="min-h-screen flex flex-col retro-grid-bg selection:bg-purple-500 selection:text-white">
    <Navbar />

    <main class="grow">
      <HeroSection />
      <AboutSection />
      <SkillsSection />
      <ExperienceSection />
      <ProjectsSection />
    </main>

    <Footer />
  </div>
</template>