<template>
  <nav class="navbar">
    <div class="container">
      <a href="#home" class="logo">AL</a>
      <div class="navbar-links" :class="{ active: mobileMenuOpen }">
        <a 
          v-for="link in navLinks" 
          :key="link.id"
          :href="link.href"
          @click="handleNavClick(link.id)"
          :class="{ active: activeSection === link.id }"
        >
          <i :class="link.icon"></i> {{ link.text }}
        </a>
      </div>
      <button class="navbar-toggle" @click="toggleMobileMenu">
        <i class="fas fa-bars"></i>
      </button>
    </div>
  </nav>
</template>

<script>
export default {
  name: 'AppNavbar',
  data() {
    return {
      mobileMenuOpen: false,
      activeSection: 'home',
      navLinks: [
        { id: 'home', href: '#home', icon: 'fas fa-home', text: 'Accueil' },
        { id: 'about', href: '#about', icon: 'fas fa-user', text: 'À propos' },
        { id: 'skills', href: '#skills', icon: 'fas fa-code', text: 'Compétences' },
        { id: 'projects', href: '#projects', icon: 'fas fa-project-diagram', text: 'Projets' },
        { id: 'contact', href: '#contact', icon: 'fas fa-envelope', text: 'Contact' }
      ]
    }
  },
  methods: {
    toggleMobileMenu() {
      this.mobileMenuOpen = !this.mobileMenuOpen
    },
    handleNavClick(sectionId) {
      this.activeSection = sectionId
      this.mobileMenuOpen = false
    },
    handleScroll() {
      const sections = ['home', 'about', 'skills', 'projects', 'contact']
      const scrollPosition = window.scrollY + 200
      
      for (const section of sections) {
        const element = document.getElementById(section)
        if (element) {
          const offsetTop = element.offsetTop
          const offsetHeight = element.offsetHeight
          
          if (scrollPosition >= offsetTop && scrollPosition < offsetTop + offsetHeight) {
            this.activeSection = section
            break
          }
        }
      }
    }
  },
  mounted() {
    window.addEventListener('scroll', this.handleScroll)
  },
  beforeUnmount() {
  window.removeEventListener('scroll', this.handleScroll)
}
}
</script>

<style scoped>
/* Vos styles CSS pour la navbar */
.navbar {
  background-color: rgba(18, 18, 18, 0.95);
  position: fixed;
  width: 100%;
  z-index: 1000;
  padding: 1rem 0;
}

/* ... autres styles ... */
</style>