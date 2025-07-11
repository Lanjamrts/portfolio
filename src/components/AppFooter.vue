<template>
  <footer>
    <div class="container">
      <div class="footer-content">
        <div class="footer-about">
          <h3>Adrianjatovo Lanja</h3>
          <p>Étudiant en Génie Logiciel passionné par le développement web et la création de solutions innovantes.</p>
        </div>
        <div class="footer-links">
          <h3>Liens rapides</h3>
          <ul>
            <li v-for="link in quickLinks" :key="link.text">
              <a :href="link.href">{{ link.text }}</a>
            </li>
          </ul>
        </div>
        <div class="footer-contact">
          <h3>Contact</h3>
          <ul>
            <li v-for="contact in contacts" :key="contact.text">
              <i :class="contact.icon"></i> {{ contact.text }}
            </li>
          </ul>
        </div>
      </div>
      <div class="footer-bottom">
        <p>&copy; {{ currentYear }} Adrianjatovo Lanja. Tous droits réservés.</p>
        <div class="footer-social">
          <a v-for="social in socialLinks" :key="social.icon" :href="social.url" target="_blank">
            <i :class="social.icon"></i>
          </a>
        </div>
      </div>
    </div>
  </footer>
</template>

<script>
export default {
  name: 'AppFooter',
  data() {
    return {
      quickLinks: [
        { text: 'Accueil', href: '#home' },
        { text: 'À propos', href: '#about' },
        { text: 'Compétences', href: '#skills' },
        { text: 'Projets', href: '#projects' },
        { text: 'Contact', href: '#contact' }
      ],
      contacts: [
        { icon: 'fas fa-phone', text: '+261 38 95 983 72' },
        { icon: 'fas fa-envelope', text: 'lanjaadrianjatovo@gmail.com' },
        { icon: 'fas fa-map-marker-alt', text: 'Antananarivo, Madagascar' }
      ],
      socialLinks: [
        { icon: 'fab fa-github', url: 'https://github.com/lanjamrts' },
        { icon: 'fab fa-linkedin', url: '#' },
        { icon: 'fab fa-twitter', url: '#' }
      ]
    }
  },
  computed: {
    currentYear() {
      return new Date().getFullYear()
    }
  }
}
</script>

<style scoped>
footer {
  background-color: var(--dark-light);
  padding: 3rem 0 1.5rem;
}

.footer-content {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 2rem;
  margin-bottom: 2rem;
}

.footer-about h3 {
  font-size: 1.5rem;
  margin-bottom: 1rem;
  color: var(--primary);
}

.footer-links h3, .footer-contact h3 {
  font-size: 1.5rem;
  margin-bottom: 1rem;
  color: var(--primary);
}

.footer-links ul, .footer-contact ul {
  list-style: none;
}

.footer-links li, .footer-contact li {
  margin-bottom: 0.8rem;
}

.footer-links a {
  color: var(--light);
  text-decoration: none;
  transition: color 0.3s;
}

.footer-links a:hover {
  color: var(--primary);
}

.footer-contact li {
  display: flex;
  align-items: center;
  gap: 0.8rem;
}

.footer-bottom {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding-top: 1.5rem;
  border-top: 1px solid var(--secondary);
}

.footer-social {
  display: flex;
  gap: 1rem;
}

.footer-social a {
  color: var(--light);
  font-size: 1.2rem;
  transition: color 0.3s;
}

.footer-social a:hover {
  color: var(--primary);
}

@media (max-width: 576px) {
  .footer-bottom {
    flex-direction: column;
    gap: 1rem;
  }
}
</style>