<template>
  <footer class="footer">
    <div class="footer-bg">
      <div class="footer-decoration">
        <div class="decoration-circle circle-1"></div>
        <div class="decoration-circle circle-2"></div>
        <div class="decoration-circle circle-3"></div>
      </div>
    </div>
    
    <div class="container">
      <div class="footer-content">
        <div class="footer-section footer-about" data-aos="fade-up" data-aos-delay="100">
          <div class="section-header">
            <h3 class="section-title">Adrianjatovo Lanja</h3>
            <div class="title-underline"></div>
          </div>
          <p class="about-description">
            Étudiant en Génie Logiciel passionné par le développement web et la création de solutions innovantes. 
            Toujours en quête d'apprentissage et de nouvelles technologies.
          </p>
          <div class="tech-highlights">
            <span class="tech-tag">Vue.js</span>
            <span class="tech-tag">JavaScript</span>
            <span class="tech-tag">Python</span>
            <span class="tech-tag">Java</span>
          </div>
        </div>

        <div class="footer-section footer-links" data-aos="fade-up" data-aos-delay="200">
          <div class="section-header">
            <h3 class="section-title">Navigation</h3>
            <div class="title-underline"></div>
          </div>
          <ul class="links-list">
            <li v-for="link in quickLinks" :key="link.text" class="link-item">
              <a :href="link.href" class="footer-link">
                <i :class="link.icon"></i>
                <span>{{ link.text }}</span>
                <div class="link-hover"></div>
              </a>
            </li>
          </ul>
        </div>

        <div class="footer-section footer-contact" data-aos="fade-up" data-aos-delay="300">
          <div class="section-header">
            <h3 class="section-title">Contact</h3>
            <div class="title-underline"></div>
          </div>
          <ul class="contact-list">
            <li v-for="contact in contacts" :key="contact.text" class="contact-item">
              <div class="contact-icon">
                <i :class="contact.icon"></i>
              </div>
              <div class="contact-info">
                <span class="contact-label">{{ contact.label }}</span>
                <span class="contact-value">{{ contact.text }}</span>
              </div>
            </li>
          </ul>
        </div>
      </div>

      <div class="footer-divider"></div>

      <div class="footer-bottom" data-aos="fade-up" data-aos-delay="400">
        <div class="copyright">
          <p>&copy; {{ currentYear }} Adrianjatovo Lanja. Tous droits réservés.</p>
        </div>
        
        <div class="footer-social">
          <a 
            v-for="social in socialLinks" 
            :key="social.icon" 
            :href="social.url" 
            :target="social.target"
            :title="social.title"
            class="social-link"
          >
            <i :class="social.icon"></i>
            <div class="social-hover"></div>
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
        { text: 'Accueil', href: '#home', icon: 'fas fa-home' },
        { text: 'À propos', href: '#about', icon: 'fas fa-user' },
        { text: 'Compétences', href: '#skills', icon: 'fas fa-code' },
        { text: 'Projets', href: '#projects', icon: 'fas fa-briefcase' },
        { text: 'Contact', href: '#contact', icon: 'fas fa-envelope' }
      ],
      contacts: [
        { 
          icon: 'fas fa-phone', 
          text: '+261 38 95 983 72',
          label: 'Téléphone'
        },
        { 
          icon: 'fas fa-envelope', 
          text: 'lanjaadrianjatovo@gmail.com',
          label: 'Email'
        },
        { 
          icon: 'fas fa-map-marker-alt', 
          text: 'Antananarivo, Madagascar',
          label: 'Localisation'
        }
      ],
      socialLinks: [
        { 
          icon: 'fab fa-github', 
          url: 'https://github.com/lanjamrts',
          target: '_blank',
          title: 'GitHub'
        },
        { 
          icon: 'fab fa-linkedin', 
          url: '#',
          target: '_blank',
          title: 'LinkedIn'
        },
        { 
          icon: 'fab fa-twitter', 
          url: '#',
          target: '_blank',
          title: 'Twitter'
        }
      ]
    }
  },
  computed: {
    currentYear() {
      return new Date().getFullYear()
    }
  },
  mounted() {
    this.initAnimations();
  },
  methods: {
    initAnimations() {
      // Animation des éléments avec Intersection Observer
      const elements = document.querySelectorAll(
        '.footer-section, .footer-bottom'
      );

      elements.forEach(el => {
        el.style.opacity = '0';
        el.style.transform = 'translateY(30px)';
      });

      const observer = new IntersectionObserver((entries) => {
        entries.forEach((entry, index) => {
          if (entry.isIntersecting) {
            setTimeout(() => {
              entry.target.style.transition = 'all 0.8s cubic-bezier(0.4, 0, 0.2, 1)';
              entry.target.style.opacity = '1';
              entry.target.style.transform = 'translateY(0)';
            }, index * 150);
            observer.unobserve(entry.target);
          }
        });
      }, { threshold: 0.1 });

      elements.forEach(el => observer.observe(el));
    }
  }
}
</script>

<style scoped>
.footer {
  position: relative;
  background: linear-gradient(135deg, #0a0a0a 0%, #1a1a1a 50%, #0f0f0f 100%);
  padding: 4rem 0 2rem;
  overflow: hidden;
}

.footer-bg {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 1;
}

.footer-decoration {
  position: relative;
  width: 100%;
  height: 100%;
}

.decoration-circle {
  position: absolute;
  border-radius: 50%;
  background: linear-gradient(135deg, rgba(102, 126, 234, 0.05), rgba(118, 75, 162, 0.05));
  animation: float 8s ease-in-out infinite;
}

.circle-1 {
  width: 120px;
  height: 120px;
  top: 10%;
  left: 5%;
  animation-delay: 0s;
}

.circle-2 {
  width: 80px;
  height: 80px;
  top: 60%;
  right: 10%;
  animation-delay: 3s;
}

.circle-3 {
  width: 100px;
  height: 100px;
  bottom: 20%;
  left: 15%;
  animation-delay: 6s;
}

@keyframes float {
  0%, 100% {
    transform: translateY(0px) rotate(0deg);
  }
  50% {
    transform: translateY(-15px) rotate(180deg);
  }
}

.container {
  position: relative;
  z-index: 2;
}

.footer-content {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 3rem;
  margin-bottom: 3rem;
}

.footer-section {
  opacity: 0;
  transform: translateY(30px);
}

.section-header {
  margin-bottom: 1.5rem;
}

.section-title {
  font-size: 1.8rem;
  font-weight: 700;
  margin-bottom: 0.5rem;
  background: linear-gradient(135deg, #64ffda 0%, #233554 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.title-underline {
  width: 50px;
  height: 3px;
  background: linear-gradient(135deg, #64ffda 0%, #233554 100%);
  border-radius: 2px;
  margin-top: 0.5rem;
}

.about-description {
  font-size: 1rem;
  line-height: 1.7;
  color: #8892b0;
  margin-bottom: 1.5rem;
}

.tech-highlights {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
}

.tech-tag {
  padding: 0.3rem 0.8rem;
  background: rgba(102, 126, 234, 0.1);
  border: 1px solid rgba(102, 126, 234, 0.3);
  border-radius: 20px;
  font-size: 0.8rem;
  color: #64ffda;
  transition: all 0.3s ease;
}

.tech-tag:hover {
  background: rgba(102, 126, 234, 0.2);
  transform: translateY(-2px);
}

.links-list, .contact-list {
  list-style: none;
  padding: 0;
}

.link-item, .contact-item {
  margin-bottom: 1rem;
}

.footer-link {
  display: flex;
  align-items: center;
  gap: 0.8rem;
  color: #8892b0;
  text-decoration: none;
  font-size: 1rem;
  transition: all 0.3s ease;
  position: relative;
  padding: 0.5rem 0;
}

.footer-link i {
  color: #64ffda;
  font-size: 1.1rem;
  width: 20px;
  text-align: center;
}

.footer-link:hover {
  color: #e6f1ff;
  transform: translateX(5px);
}

.footer-link:hover i {
  color: #233554;
}

.link-hover {
  position: absolute;
  bottom: 0;
  left: 0;
  width: 0;
  height: 2px;
  background: linear-gradient(135deg, #64ffda 0%, #233554 100%);
  transition: width 0.3s ease;
}

.footer-link:hover .link-hover {
  width: 100%;
}

.contact-item {
  display: flex;
  align-items: flex-start;
  gap: 1rem;
  margin-bottom: 1.2rem;
}

.contact-icon {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 40px;
  height: 40px;
  background: rgba(102, 126, 234, 0.1);
  border-radius: 10px;
  color: #64ffda;
  font-size: 1.1rem;
  transition: all 0.3s ease;
}

.contact-item:hover .contact-icon {
  background: rgba(102, 126, 234, 0.2);
  transform: scale(1.1);
}

.contact-info {
  display: flex;
  flex-direction: column;
  gap: 0.2rem;
}

.contact-label {
  font-size: 0.8rem;
  color: #64ffda;
  font-weight: 600;
}

.contact-value {
  font-size: 0.9rem;
  color: #8892b0;
}

.footer-divider {
  height: 1px;
  background: linear-gradient(90deg, transparent, rgba(102, 126, 234, 0.3), transparent);
  margin: 2rem 0;
}

.footer-bottom {
  display: flex;
  justify-content: space-between;
  align-items: center;
  opacity: 0;
  transform: translateY(30px);
}

.copyright {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.copyright p {
  color: #8892b0;
  font-size: 0.9rem;
  margin: 0;
}

.made-with {
  color: #64ffda;
  font-size: 0.8rem;
  display: flex;
  align-items: center;
  gap: 0.3rem;
}

.made-with i {
  color: #ea4335;
  animation: heartbeat 2s ease-in-out infinite;
}

@keyframes heartbeat {
  0%, 100% {
    transform: scale(1);
  }
  50% {
    transform: scale(1.2);
  }
}

.footer-social {
  display: flex;
  gap: 1rem;
}

.social-link {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 45px;
  height: 45px;
  border-radius: 12px;
  color: #8892b0;
  font-size: 1.2rem;
  text-decoration: none;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  position: relative;
  overflow: hidden;
  background: rgba(255, 255, 255, 0.05);
  backdrop-filter: blur(10px);
}

.social-link::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: linear-gradient(135deg, var(--social-color), var(--social-color-dark));
  opacity: 0;
  transition: opacity 0.3s;
}

.social-link:hover::before {
  opacity: 1;
}

.social-link i {
  position: relative;
  z-index: 1;
}

.social-link:nth-child(1) {
  --social-color: #333;
  --social-color-dark: #24292e;
}

.social-link:nth-child(2) {
  --social-color: #0077b5;
  --social-color-dark: #005885;
}

.social-link:nth-child(3) {
  --social-color: #1da1f2;
  --social-color-dark: #0d8bd9;
}

.social-link:hover {
  transform: translateY(-5px) scale(1.1);
  box-shadow: 0 10px 25px rgba(0, 0, 0, 0.3);
  color: #e6f1ff;
}

/* Responsive Design */
@media (max-width: 992px) {
  .footer-content {
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 2rem;
  }
}

@media (max-width: 768px) {
  .footer {
    padding: 3rem 0 1.5rem;
  }
  
  .footer-content {
    grid-template-columns: 1fr;
    gap: 2rem;
  }
  
  .section-title {
    font-size: 1.5rem;
  }
  
  .footer-bottom {
    flex-direction: column;
    gap: 1.5rem;
    text-align: center;
  }
  
  .footer-social {
    justify-content: center;
  }
}

@media (max-width: 576px) {
  .tech-highlights {
    justify-content: center;
  }
  
  .contact-item {
    flex-direction: column;
    align-items: flex-start;
    gap: 0.5rem;
  }
  
  .contact-icon {
    width: 35px;
    height: 35px;
    font-size: 1rem;
  }
}
</style>