<template>
  <section id="about" class="about-section">
    <div class="container">
      <div class="section-header">
        <h2 class="section-title">À <span>propos</span></h2>
        <p class="section-subtitle">Découvrez mon parcours et ma passion pour le développement</p>
      </div>
      
      <div class="about-content">
        <div class="about-text">
          <div class="intro-block">
            <h3 class="greeting">👋 Bonjour, je suis</h3>
            <h2 class="name">ANDRIANJATOVO Lanja Mirantsoa</h2>
            <h4 class="title">Développeur Full-Stack en formation</h4>
          </div>
          
          <div class="description">
            <p class="main-description">
              Passionné par le développement web et les technologies modernes, je suis actuellement étudiant en Génie Logiciel à l'INSI Ambanidia. 
              Mon objectif est de créer des applications web performantes et des expériences utilisateur exceptionnelles.
            </p>
            
            <div class="tech-stack">
              <h4>🛠️ Technologies maîtrisées</h4>
              <div class="tech-grid">
                <div class="tech-item" v-for="tech in technologies" :key="tech.name">
                  <i :class="tech.icon"></i>
                  <span>{{ tech.name }}</span>
                </div>
              </div>
            </div>
          </div>
          
          <div class="stats-grid">
            <div class="stat-item" v-for="stat in stats" :key="stat.label">
              <div class="stat-number" :data-target="stat.value">0</div>
              <div class="stat-label">{{ stat.label }}</div>
            </div>
          </div>
          
          <div class="about-details">
            <div class="detail-card">
              <div class="detail-header">
                <i class="fas fa-user"></i>
                <h5>Informations personnelles</h5>
              </div>
              <div class="detail-content">
                <div class="detail-row">
                  <span class="label">Nom complet :</span>
                  <span class="value">ANDRIANJATOVO Lanja Mirantsoa</span>
                </div>
                <div class="detail-row">
                  <span class="label">Email :</span>
                  <span class="value">lanjaadrianjatovo@gmail.com</span>
                </div>
                <div class="detail-row">
                  <span class="label">Téléphone :</span>
                  <span class="value">+261 38 95 983 72</span>
                </div>
                <div class="detail-row">
                  <span class="label">Localisation :</span>
                  <span class="value">Antananarivo, Madagascar</span>
                </div>
              </div>
            </div>
            
            <div class="detail-card">
              <div class="detail-header">
                <i class="fas fa-graduation-cap"></i>
                <h5>Formation</h5>
              </div>
              <div class="detail-content">
                <div class="education-item">
                  <div class="education-year">2022 - Présent</div>
                  <div class="education-info">
                    <h6>Génie Logiciel</h6>
                    <p>INSI Ambanidia - 2ème année</p>
                  </div>
                </div>
              </div>
            </div>
          </div>
          
          <div class="cta-section">
            <p class="cta-text">Je recherche activement un stage pour mettre en pratique mes compétences et contribuer à des projets innovants.</p>
            <div class="cta-buttons">
              <a href="#contact" class="btn btn-primary">
                <i class="fas fa-envelope"></i>
                <span>Me contacter</span>
              </a>
              <a href="/cv-lanja.pdf" class="btn btn-secondary">
                <i class="fas fa-download"></i>
                <span>Voir mon CV</span>
              </a>
            </div>
          </div>
        </div>
        
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'AboutSection',
  data() {
    return {
      technologies: [
        { name: 'HTML5', icon: 'fab fa-html5' },
        { name: 'CSS3', icon: 'fab fa-css3-alt' },
        { name: 'JavaScript', icon: 'fab fa-js' },
        { name: 'Vue.js', icon: 'fab fa-vuejs' },
        { name: 'Angular', icon: 'fab fa-angular' },
        { name: 'PHP', icon: 'fab fa-php' },
        { name: 'React', icon: 'fab fa-react' },
        { name: 'Node.js', icon: 'fab fa-node-js' }
      ],
      stats: [
        { label: 'Projets réalisés', value: 15 },
        { label: 'Technologies maîtrisées', value: 8 },
        { label: 'Mois d\'expérience', value: 18 },
        { label: 'Satisfaction client', value: 95 }
      ],
      experience: []
    };
  },
  mounted() {
    this.initAnimations();
    this.animateStats();
  },
  methods: {
    initAnimations() {
      const elements = document.querySelectorAll(
        '.intro-block, .description, .stats-grid, .about-details, .cta-section'
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
            }, index * 200);
            observer.unobserve(entry.target);
          }
        });
      }, { threshold: 0.2 });

      elements.forEach(el => observer.observe(el));
    },
    
    animateStats() {
      const statNumbers = document.querySelectorAll('.stat-number');
      
      const observer = new IntersectionObserver((entries) => {
        entries.forEach(entry => {
          if (entry.isIntersecting) {
            const target = parseInt(entry.target.getAttribute('data-target'));
            const duration = 2000;
            const increment = target / (duration / 16);
            let current = 0;
            
            const timer = setInterval(() => {
              current += increment;
              if (current >= target) {
                current = target;
                clearInterval(timer);
              }
              entry.target.textContent = Math.floor(current);
            }, 16);
            
            observer.unobserve(entry.target);
          }
        });
      }, { threshold: 0.5 });
      
      statNumbers.forEach(stat => observer.observe(stat));
    }
  }
};
</script>

<style scoped>
.about-section {
  position: relative;
  overflow: hidden;
  background: #0a192f;
  padding: 6rem 0;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 2rem;
}

.section-header {
  text-align: center;
  margin-bottom: 4rem;
}

.section-title {
  font-size: 3rem;
  font-weight: 700;
  margin-bottom: 1rem;
  color: #64ffda;
}

.section-title span {
  color: #64ffda;
}

.section-subtitle {
  font-size: 1.2rem;
  color: #8892b0;
  max-width: 600px;
  margin: 0 auto;
}

.about-content {
  display: grid;
  grid-template-columns: 1fr;
  gap: 2rem;
  align-items: start;
}

.intro-block {
  margin-bottom: 2rem;
}

.greeting {
  font-size: 1.2rem;
  color: #64ffda;
  margin-bottom: 0.5rem;
}

.name {
  font-size: 3rem;
  font-weight: 700;
  margin-bottom: 0.5rem;
  color: #e6f1ff;
}

.title {
  font-size: 1.5rem;
  color: #8892b0;
  margin-bottom: 2rem;
}

.description {
  margin-bottom: 3rem;
}

.main-description {
  font-size: 1.1rem;
  line-height: 1.8;
  color: #e6f1ff;
  margin-bottom: 2rem;
}

.tech-stack {
  margin-bottom: 2rem;
}

.tech-stack h4 {
  color: #64ffda;
  margin-bottom: 1rem;
}

.tech-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(120px, 1fr));
  gap: 1rem;
}

.tech-item {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.8rem;
  background: #112240;
  border-radius: 8px;
  border: 1px solid #233554;
  transition: all 0.3s ease;
}

.tech-item:hover {
  background: #233554;
  transform: translateY(-2px);
}

.tech-item i {
  font-size: 1.2rem;
  color: #64ffda;
}

.tech-item span {
  font-size: 0.9rem;
  color: #e6f1ff;
}

.stats-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 1.5rem;
  margin-bottom: 3rem;
}

.stat-item {
  text-align: center;
  padding: 1.5rem;
  background: #112240;
  border-radius: 12px;
  border: 1px solid #233554;
  transition: all 0.3s ease;
}

.stat-item:hover {
  transform: translateY(-5px);
  background: #233554;
}

.stat-number {
  font-size: 2.5rem;
  font-weight: 700;
  color: #64ffda;
  margin-bottom: 0.5rem;
}

.stat-label {
  font-size: 0.9rem;
  color: #8892b0;
}

.about-details {
  display: grid;
  gap: 1.5rem;
  margin-bottom: 3rem;
}

.detail-card {
  background: #112240;
  border-radius: 12px;
  padding: 1.5rem;
  border: 1px solid #233554;
  transition: all 0.3s ease;
}

.detail-card:hover {
  transform: translateY(-3px);
  background: #233554;
}

.detail-header {
  display: flex;
  align-items: center;
  gap: 0.8rem;
  margin-bottom: 1rem;
}

.detail-header i {
  font-size: 1.2rem;
  color: #64ffda;
}

.detail-header h5 {
  font-size: 1.1rem;
  color: #64ffda;
  margin: 0;
}

.detail-content {
  display: flex;
  flex-direction: column;
  gap: 0.8rem;
}

.detail-row {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.detail-row .label {
  font-weight: 600;
  color: #8892b0;
}

.detail-row .value {
  color: #e6f1ff;
}

.education-item {
  display: flex;
  gap: 1rem;
  align-items: flex-start;
}

.education-year {
  background: #233554;
  color: #64ffda;
  padding: 0.3rem 0.8rem;
  border-radius: 20px;
  font-size: 0.8rem;
  font-weight: 600;
}

.education-info h6 {
  color: #64ffda;
  margin: 0 0 0.3rem 0;
}

.education-info p {
  color: #e6f1ff;
  margin: 0;
}

.cta-section {
  text-align: center;
  margin-bottom: 2rem;
}

.cta-text {
  color: #e6f1ff;
  margin-bottom: 2rem;
  font-size: 1.1rem;
}

.cta-buttons {
  display: flex;
  gap: 1rem;
  justify-content: center;
  flex-wrap: wrap;
}

.btn {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  padding: 1rem 2rem;
  border-radius: 8px;
  text-decoration: none;
  font-weight: 600;
  transition: all 0.3s ease;
  border: 2px solid transparent;
}

.btn-primary {
  background: #64ffda;
  color: #0a192f;
}

.btn-primary:hover {
  transform: translateY(-2px);
  box-shadow: 0 10px 20px rgba(100, 255, 218, 0.2);
}

.btn-secondary {
  background: transparent;
  color: #64ffda;
  border-color: #64ffda;
}

.btn-secondary:hover {
  background: #64ffda;
  color: #0a192f;
  transform: translateY(-2px);
}

@media (max-width: 992px) {
  .about-content {
    grid-template-columns: 1fr;
    gap: 3rem;
  }
  .name {
    font-size: 2.5rem;
  }
  .stats-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}
@media (max-width: 768px) {
  .name {
    font-size: 2rem;
  }
  .title {
    font-size: 1.2rem;
  }
  .stats-grid {
    grid-template-columns: 1fr;
  }
  .tech-grid {
    grid-template-columns: repeat(2, 1fr);
  }
  .cta-buttons {
    flex-direction: column;
    align-items: center;
  }
  .btn {
    width: 100%;
    max-width: 300px;
  }
}
@media (max-width: 576px) {
  .tech-grid {
    grid-template-columns: 1fr;
  }
  .detail-row {
    flex-direction: column;
    align-items: flex-start;
    gap: 0.3rem;
  }
}
</style> 