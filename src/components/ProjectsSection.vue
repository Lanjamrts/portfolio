<template>
  <section id="projects" class="projects-section">
    <div class="container">
      <div class="section-header">
        <h2 class="section-title">Mes <span>Projets</span></h2>
      </div>
      
      <div class="projects-grid">
        <div 
          class="project-card" 
          v-for="project in projects" 
          :key="project.id"
          :data-category="project.category"
        >
          <div class="project-image">
            <img :src="project.image" :alt="project.title">
            <div class="project-overlay">
              <div class="project-links">
                <a :href="project.demoUrl" class="link-icon" target="_blank" :title="'Voir le projet'">
                  <i class="fas fa-external-link-alt"></i>
                </a>
                <a :href="project.githubUrl" class="link-icon" target="_blank" :title="'Code source'">
                  <i class="fab fa-github"></i>
                </a>
              </div>
              <div class="project-category">
                <span>{{ getCategoryLabel(project.category) }}</span>
              </div>
            </div>
            <div class="project-badge">
              <i :class="project.badgeIcon"></i>
            </div>
          </div>
          
          <div class="project-content">
            <div class="project-header">
              <h3 class="project-title">{{ project.title }}</h3>
              <div class="project-rating">
                <i v-for="i in 5" :key="i" class="fas fa-star" :class="{ filled: i <= project.rating }"></i>
              </div>
            </div>
            
            <p class="project-description">{{ project.description }}</p>
            
            <div class="project-features">
              <div class="feature-item" v-for="feature in project.features" :key="feature">
                <i class="fas fa-check"></i>
                <span>{{ feature }}</span>
              </div>
            </div>
            
            <div class="project-tech">
              <span v-for="tech in project.technologies" :key="tech" class="tech-tag">
                <i :class="getTechIcon(tech)"></i>
                {{ tech }}
              </span>
            </div>
            
            <div class="project-footer">
              <div class="project-date">
                <i class="fas fa-calendar"></i>
                <span>{{ project.date }}</span>
              </div>
              <div class="project-status" :class="project.status">
                <i :class="getStatusIcon(project.status)"></i>
                <span>{{ getStatusLabel(project.status) }}</span>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <!-- Background decoration -->
    <div class="bg-decoration">
      <div class="project-particles">
        <div class="particle" v-for="i in 12" :key="i" :style="{ animationDelay: `${i * 0.3}s` }"></div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'ProjectsSection',
  data() {
    return {
      projects: [
        {
          id: 1,
          title: 'Site E-commerce',
          description: 'Plateforme de commerce électronique complète avec gestion des produits, panier d\'achat, système de paiement et interface d\'administration.',
          category: 'web',
          technologies: ['.NET', 'C#', 'SQL Server', 'Bootstrap'],
          image: require('@/assets/images/e-commerce.png'),
          demoUrl: '#',
          githubUrl: '#',
          rating: 5,
          date: 'Décembre 2023',
          status: 'completed',
          badgeIcon: 'fas fa-shopping-cart',
          features: [
            'Gestion des produits',
            'Système de panier',
            'Interface admin',
            'Paiement sécurisé'
          ]
        },
        {
          id: 2,
          title: 'Application Météo',
          description: 'Application web de prévisions météorologiques en temps réel avec géolocalisation et interface utilisateur moderne et intuitive.',
          category: 'academic',
          technologies: ['Angular', 'TypeScript', 'API REST', 'CSS3'],
          image: require('@/assets/images/la-meteo.png'),
          demoUrl: '#',
          githubUrl: '#',
          rating: 4,
          date: 'Novembre 2023',
          status: 'completed',
          badgeIcon: 'fas fa-cloud-sun',
          features: [
            'Prévisions temps réel',
            'Géolocalisation',
            'Interface responsive',
            'API météo'
          ]
        },
        {
          id: 3,
          title: 'Architecture Microservices',
          description: 'Application web conçue selon une architecture de microservices avec conteneurisation Docker pour une scalabilité optimale.',
          category: 'web',
          technologies: ['Docker', 'Microservices', 'API Gateway', 'Containers'],
          image: require('@/assets/images/microservice.png'),
          demoUrl: '#',
          githubUrl: '#',
          rating: 5,
          date: 'Octobre 2023',
          status: 'completed',
          badgeIcon: 'fas fa-cubes',
          features: [
            'Architecture distribuée',
            'Conteneurisation',
            'Scalabilité',
            'Haute disponibilité'
          ]
        }
      ]
    }
  },

  mounted() {
    this.initAnimations();
  },
  methods: {
    getCategoryLabel(category) {
      const labels = {
        'web': 'Développement Web',
        'mobile': 'Application Mobile',
        'academic': 'Projet Académique'
      };
      return labels[category] || category;
    },
    
    getTechIcon(tech) {
      const icons = {
        '.NET': 'fab fa-microsoft',
        'C#': 'fas fa-code',
        'Angular': 'fab fa-angular',
        'TypeScript': 'fab fa-js',
        'Docker': 'fab fa-docker',
        'SQL Server': 'fas fa-database',
        'Bootstrap': 'fab fa-bootstrap',
        'API REST': 'fas fa-server',
        'CSS3': 'fab fa-css3-alt',
        'Microservices': 'fas fa-cubes',
        'API Gateway': 'fas fa-route',
        'Containers': 'fas fa-box'
      };
      return icons[tech] || 'fas fa-code';
    },
    
    getStatusIcon(status) {
      const icons = {
        'completed': 'fas fa-check-circle',
        'in-progress': 'fas fa-clock',
        'planned': 'fas fa-calendar-plus'
      };
      return icons[status] || 'fas fa-info-circle';
    },
    
    getStatusLabel(status) {
      const labels = {
        'completed': 'Terminé',
        'in-progress': 'En cours',
        'planned': 'Planifié'
      };
      return labels[status] || status;
    },
    
    initAnimations() {
      const elements = document.querySelectorAll(
        '.project-card'
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
      }, { threshold: 0.2 });

      elements.forEach(el => observer.observe(el));
    }
  }
}
</script>

<style scoped>
.projects-section {
  position: relative;
  overflow: hidden;
  background: linear-gradient(135deg, #0a0a0a 0%, #1a1a1a 50%, #0f0f0f 100%);
}

.section-header {
  text-align: center;
  margin-bottom: 4rem;
}



.projects-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(380px, 1fr));
  gap: 2.5rem;
  margin-bottom: 4rem;
}

.project-card {
  background: rgba(255, 255, 255, 0.05);
  border-radius: 20px;
  overflow: hidden;
  transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
  border: 1px solid rgba(255, 255, 255, 0.1);
  position: relative;
}

.project-card:hover {
  transform: translateY(-10px) scale(1.02);
  box-shadow: 0 20px 40px rgba(0, 0, 0, 0.3);
  border-color: rgba(102, 126, 234, 0.3);
}

.project-image {
  position: relative;
  height: 250px;
  overflow: hidden;
}

.project-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.6s cubic-bezier(0.4, 0, 0.2, 1);
}

.project-card:hover .project-image img {
  transform: scale(1.1);
}

.project-overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: linear-gradient(135deg, rgba(102, 126, 234, 0.9), rgba(118, 75, 162, 0.9));
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  opacity: 0;
  transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
  padding: 2rem;
}

.project-card:hover .project-overlay {
  opacity: 1;
}

.project-links {
  display: flex;
  gap: 1rem;
  justify-content: center;
}

.link-icon {
  color: white;
  font-size: 1.2rem;
  width: 50px;
  height: 50px;
  border-radius: 50%;
  background: rgba(255, 255, 255, 0.2);
  display: flex;
  justify-content: center;
  align-items: center;
  transition: all 0.3s ease;
  backdrop-filter: blur(10px);
}

.link-icon:hover {
  transform: scale(1.2);
  background: rgba(255, 255, 255, 0.3);
}

.project-category {
  text-align: center;
}

.project-category span {
  background: rgba(255, 255, 255, 0.2);
  color: white;
  padding: 0.5rem 1rem;
  border-radius: 20px;
  font-size: 0.9rem;
  font-weight: 600;
  backdrop-filter: blur(10px);
}

.project-badge {
  position: absolute;
  top: 1rem;
  right: 1rem;
  width: 40px;
  height: 40px;
  background: linear-gradient(135deg, #667eea, #764ba2);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
  font-size: 1rem;
  box-shadow: 0 4px 15px rgba(102, 126, 234, 0.3);
}

.project-content {
  padding: 2rem;
}

.project-header {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  margin-bottom: 1rem;
}

.project-title {
  font-size: 1.4rem;
  color: #ffffff;
  margin: 0;
  font-weight: 600;
}

.project-rating {
  display: flex;
  gap: 0.2rem;
}

.project-rating i {
  color: #a0a0a0;
  font-size: 0.9rem;
}

.project-rating i.filled {
  color: #ffd700;
}

.project-description {
  color: #b0b0b0;
  line-height: 1.6;
  margin-bottom: 1.5rem;
  font-size: 0.95rem;
}

.project-features {
  margin-bottom: 1.5rem;
}

.feature-item {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  margin-bottom: 0.5rem;
  font-size: 0.9rem;
  color: #a0a0a0;
}

.feature-item i {
  color: #667eea;
  font-size: 0.8rem;
}

.project-tech {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
  margin-bottom: 1.5rem;
}

.tech-tag {
  display: flex;
  align-items: center;
  gap: 0.3rem;
  background: rgba(102, 126, 234, 0.1);
  color: #667eea;
  padding: 0.4rem 0.8rem;
  border-radius: 20px;
  font-size: 0.8rem;
  font-weight: 500;
  border: 1px solid rgba(102, 126, 234, 0.2);
}

.tech-tag i {
  font-size: 0.7rem;
}

.project-footer {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding-top: 1rem;
  border-top: 1px solid rgba(255, 255, 255, 0.1);
}

.project-date {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  color: #a0a0a0;
  font-size: 0.9rem;
}

.project-status {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.3rem 0.8rem;
  border-radius: 20px;
  font-size: 0.8rem;
  font-weight: 600;
}

.project-status.completed {
  background: rgba(0, 200, 83, 0.1);
  color: #00c853;
  border: 1px solid rgba(0, 200, 83, 0.2);
}

.project-status.in-progress {
  background: rgba(255, 171, 0, 0.1);
  color: #ffab00;
  border: 1px solid rgba(255, 171, 0, 0.2);
}

.project-status.planned {
  background: rgba(102, 126, 234, 0.1);
  color: #667eea;
  border: 1px solid rgba(102, 126, 234, 0.2);
}

.bg-decoration {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
  z-index: 1;
}

.project-particles {
  position: absolute;
  width: 100%;
  height: 100%;
}

.particle {
  position: absolute;
  width: 3px;
  height: 3px;
  background: #667eea;
  border-radius: 50%;
  animation: particleFloat 8s ease-in-out infinite;
}

.particle:nth-child(1) { top: 10%; left: 10%; animation-delay: 0s; }
.particle:nth-child(2) { top: 20%; right: 15%; animation-delay: 0.5s; }
.particle:nth-child(3) { top: 40%; left: 20%; animation-delay: 1s; }
.particle:nth-child(4) { top: 60%; right: 25%; animation-delay: 1.5s; }
.particle:nth-child(5) { top: 80%; left: 15%; animation-delay: 2s; }
.particle:nth-child(6) { top: 30%; left: 80%; animation-delay: 2.5s; }
.particle:nth-child(7) { top: 70%; right: 10%; animation-delay: 3s; }
.particle:nth-child(8) { top: 50%; left: 5%; animation-delay: 3.5s; }
.particle:nth-child(9) { top: 90%; right: 30%; animation-delay: 4s; }
.particle:nth-child(10) { top: 15%; left: 60%; animation-delay: 4.5s; }
.particle:nth-child(11) { top: 85%; left: 40%; animation-delay: 5s; }
.particle:nth-child(12) { top: 25%; right: 5%; animation-delay: 5.5s; }

@keyframes particleFloat {
  0%, 100% {
    transform: translateY(0px) scale(1);
    opacity: 0.3;
  }
  50% {
    transform: translateY(-15px) scale(1.2);
    opacity: 1;
  }
}

/* Responsive Design */
@media (max-width: 992px) {
  .projects-grid {
    grid-template-columns: repeat(auto-fill, minmax(320px, 1fr));
    gap: 2rem;
  }
}

@media (max-width: 768px) {
  .projects-grid {
    grid-template-columns: 1fr;
  }
  
  .project-header {
    flex-direction: column;
    gap: 1rem;
  }
  
  .project-footer {
    flex-direction: column;
    gap: 1rem;
    align-items: flex-start;
  }
}

@media (max-width: 576px) {
  .project-content {
    padding: 1.5rem;
  }
  
  .project-image {
    height: 200px;
  }
  
  .filter-btn {
    padding: 0.6rem 1rem;
    font-size: 0.9rem;
  }
}
</style>