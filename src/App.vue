<template>
  <div id="app">
    <AppNavbar />
    <main>
      <HomeSection />
      <StatsSection />
      <AboutSection />
      <SkillsSection />
      <ProjectsSection />
      <ContactSection />
    </main>
    <AppFooter />
  </div>
</template>

<script>
import AppNavbar from './components/AppNavbar.vue'
import AppFooter from './components/AppFooter.vue'
import HomeSection from './components/HomeSection.vue'
import StatsSection from './components/StatsSection.vue'
import AboutSection from './components/AboutSection.vue'
import SkillsSection from './components/SkillsSection.vue'
import ProjectsSection from './components/ProjectsSection.vue'
import ContactSection from './components/ContactSection.vue'

export default {
  name: 'App',
  components: {
    AppNavbar,
    AppFooter,
    HomeSection,
    StatsSection,
    AboutSection,
    SkillsSection,
    ProjectsSection,
    ContactSection
  }
}
</script>