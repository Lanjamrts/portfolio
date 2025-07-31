<template>
  <section id="skills" class="skills-section">
    <div class="container">
      <div class="section-header">
        <h2 class="section-title">Mes <span>Compétences</span></h2>
        <p class="section-subtitle">Expertise technique et niveaux de maîtrise</p>
      </div>

      <div class="skills-overview">
        <div class="skill-levels">
          <div class="level-card expert">
            <div class="level-header">
              <i class="fas fa-star"></i>
              <h3>Expert</h3>
              <span class="level-percentage">85-100%</span>
            </div>
            <div class="skills-list">
              <div class="skill-item" v-for="skill in expertSkills" :key="skill.name">
                <div class="skill-info">
                  <span class="skill-name">{{ skill.name }}</span>
                  <span class="skill-percentage">{{ skill.level }}%</span>
                </div>
                <div class="skill-bar">
                  <div class="skill-progress" :style="{ width: skill.level + '%' }"></div>
                </div>
              </div>
            </div>
          </div>

          <div class="level-card advanced">
            <div class="level-header">
              <i class="fas fa-rocket"></i>
              <h3>Avancé</h3>
              <span class="level-percentage">70-84%</span>
            </div>
            <div class="skills-list">
              <div class="skill-item" v-for="skill in advancedSkills" :key="skill.name">
                <div class="skill-info">
                  <span class="skill-name">{{ skill.name }}</span>
                  <span class="skill-percentage">{{ skill.level }}%</span>
                </div>
                <div class="skill-bar">
                  <div class="skill-progress" :style="{ width: skill.level + '%' }"></div>
                </div>
              </div>
            </div>
          </div>

          <div class="level-card intermediate">
            <div class="level-header">
              <i class="fas fa-code"></i>
              <h3>Intermédiaire</h3>
              <span class="level-percentage">50-69%</span>
            </div>
            <div class="skills-list">
              <div class="skill-item" v-for="skill in intermediateSkills" :key="skill.name">
                <div class="skill-info">
                  <span class="skill-name">{{ skill.name }}</span>
                  <span class="skill-percentage">{{ skill.level }}%</span>
                </div>
                <div class="skill-bar">
                  <div class="skill-progress" :style="{ width: skill.level + '%' }"></div>
                </div>
              </div>
            </div>
          </div>
        </div>

        <div class="specializations">
          <h3 class="specializations-title">🎯 Spécialisations</h3>
          <div class="specialization-grid">
            <div class="specialization-card" v-for="spec in specializations" :key="spec.title">
              <div class="spec-icon">
                <i :class="spec.icon"></i>
              </div>
              <div class="spec-content">
                <h4>{{ spec.title }}</h4>
                <p>{{ spec.description }}</p>
                <div class="spec-tags">
                  <span class="spec-tag" v-for="tag in spec.tags" :key="tag">{{ tag }}</span>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>



      <div class="soft-skills">
        <h3 class="soft-skills-title">💡 Compétences transversales</h3>
        <div class="soft-skills-grid">
          <div class="soft-skill-item" v-for="skill in softSkills" :key="skill.name">
            <div class="soft-skill-icon">
              <i :class="skill.icon"></i>
            </div>
            <div class="soft-skill-content">
              <h4>{{ skill.name }}</h4>
              <p>{{ skill.description }}</p>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- Background decoration -->
    <div class="bg-decoration">
      <div class="skill-particles">
        <div class="particle" v-for="i in 15" :key="i" :style="{ animationDelay: `${i * 0.2}s` }"></div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'SkillsSection',
  data() {
    return {
      expertSkills: [
        { name: 'HTML5', level: 95 },
        { name: 'CSS3', level: 90 },
        { name: 'Responsive Design', level: 88 },
        { name: 'Git/GitHub', level: 85 }
      ],
      advancedSkills: [
        { name: 'JavaScript', level: 80 },
        { name: 'Vue.js', level: 75 },
        { name: 'PHP', level: 72 },
        { name: 'Bootstrap', level: 78 }
      ],
      intermediateSkills: [
        { name: 'Angular', level: 65 },
        { name: 'Node.js', level: 60 },
        { name: 'MySQL', level: 58 },
        { name: 'React', level: 55 }
      ],
      specializations: [
        {
          title: 'Développement Frontend',
          description: 'Création d\'interfaces utilisateur modernes et interactives',
          icon: 'fas fa-laptop-code',
          tags: ['Vue.js', 'Angular', 'Responsive', 'UI/UX']
        },
        {
          title: 'Développement Backend',
          description: 'Développement d\'APIs et de services web robustes',
          icon: 'fas fa-server',
          tags: ['PHP', 'Node.js', 'APIs', 'Databases']
        },
        {
          title: 'DevOps & Outils',
          description: 'Gestion de version et déploiement d\'applications',
          icon: 'fas fa-tools',
          tags: ['Git', 'Docker', 'VS Code', 'CI/CD']
        }
      ],

      softSkills: [
        {
          name: 'Résolution de problèmes',
          description: 'Analyse et résolution efficace de problèmes techniques complexes',
          icon: 'fas fa-lightbulb'
        },
        {
          name: 'Travail d\'équipe',
          description: 'Collaboration efficace dans des projets multidisciplinaires',
          icon: 'fas fa-users'
        },
        {
          name: 'Apprentissage continu',
          description: 'Veille technologique et mise à jour constante des compétences',
          icon: 'fas fa-graduation-cap'
        },
        {
          name: 'Communication',
          description: 'Présentation claire de solutions techniques aux clients',
          icon: 'fas fa-comments'
        }
      ]
    };
  },
  mounted() {
    this.initAnimations();
  },
  methods: {
    initAnimations() {
      const elements = document.querySelectorAll(
        '.level-card, .specialization-card, .soft-skill-item'
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

      // Animation des barres de progression
      this.animateProgressBars();
    },

    animateProgressBars() {
      const progressBars = document.querySelectorAll('.skill-progress');
      
      const observer = new IntersectionObserver((entries) => {
        entries.forEach(entry => {
          if (entry.isIntersecting) {
            const targetWidth = entry.target.style.width;
            entry.target.style.width = '0%';
            
            setTimeout(() => {
              entry.target.style.transition = 'width 1.5s cubic-bezier(0.4, 0, 0.2, 1)';
              entry.target.style.width = targetWidth;
            }, 500);
            
            observer.unobserve(entry.target);
          }
        });
      }, { threshold: 0.5 });
      
      progressBars.forEach(bar => observer.observe(bar));
    }
  }
};
</script>

<style scoped>
.skills-section {
  position: relative;
  overflow: hidden;
  background: linear-gradient(135deg, #0a0a0a 0%, #1a1a1a 50%, #0f0f0f 100%);
}

.section-header {
  text-align: center;
  margin-bottom: 4rem;
}

.skills-overview {
  margin-bottom: 4rem;
}

.skill-levels {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
  gap: 2rem;
  margin-bottom: 4rem;
}

.level-card {
  background: rgba(255, 255, 255, 0.05);
  border-radius: 16px;
  padding: 2rem;
  border: 1px solid rgba(255, 255, 255, 0.1);
  transition: all 0.3s ease;
  position: relative;
  overflow: hidden;
}

.level-card::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 4px;
  background: var(--gradient-primary);
}

.level-card:hover {
  transform: translateY(-5px);
  background: rgba(255, 255, 255, 0.08);
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
}

.level-header {
  display: flex;
  align-items: center;
  gap: 1rem;
  margin-bottom: 1.5rem;
}

.level-header i {
  font-size: 1.5rem;
  color: #667eea;
}

.level-header h3 {
  font-size: 1.3rem;
  color: #ffffff;
  margin: 0;
  flex: 1;
}

.level-percentage {
  font-size: 0.9rem;
  color: #a0a0a0;
  background: rgba(102, 126, 234, 0.1);
  padding: 0.3rem 0.8rem;
  border-radius: 20px;
}

.skills-list {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.skill-item {
  margin-bottom: 1rem;
}

.skill-info {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 0.5rem;
}

.skill-name {
  color: #ffffff;
  font-weight: 500;
}

.skill-percentage {
  color: #667eea;
  font-weight: 600;
}

.skill-bar {
  height: 6px;
  background: rgba(255, 255, 255, 0.1);
  border-radius: 3px;
  overflow: hidden;
}

.skill-progress {
  height: 100%;
  background: linear-gradient(90deg, #667eea, #764ba2);
  border-radius: 3px;
  transition: width 1.5s cubic-bezier(0.4, 0, 0.2, 1);
}

.specializations {
  margin-bottom: 4rem;
}

.specializations-title {
  font-size: 1.8rem;
  color: #ffffff;
  text-align: center;
  margin-bottom: 2rem;
}

.specialization-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 2rem;
}

.specialization-card {
  background: rgba(255, 255, 255, 0.05);
  border-radius: 16px;
  padding: 2rem;
  border: 1px solid rgba(255, 255, 255, 0.1);
  transition: all 0.3s ease;
  display: flex;
  gap: 1.5rem;
  align-items: flex-start;
}

.specialization-card:hover {
  transform: translateY(-3px);
  background: rgba(255, 255, 255, 0.08);
}

.spec-icon {
  width: 50px;
  height: 50px;
  background: linear-gradient(135deg, #667eea, #764ba2);
  border-radius: 12px;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-shrink: 0;
}

.spec-icon i {
  font-size: 1.5rem;
  color: white;
}

.spec-content h4 {
  color: #ffffff;
  margin: 0 0 0.5rem 0;
  font-size: 1.2rem;
}

.spec-content p {
  color: #a0a0a0;
  margin: 0 0 1rem 0;
  line-height: 1.6;
}

.spec-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
}

.spec-tag {
  background: rgba(102, 126, 234, 0.1);
  color: #667eea;
  padding: 0.3rem 0.8rem;
  border-radius: 20px;
  font-size: 0.8rem;
  font-weight: 500;
}



.soft-skills {
  margin-bottom: 2rem;
}

.soft-skills-title {
  font-size: 1.8rem;
  color: #ffffff;
  text-align: center;
  margin-bottom: 2rem;
}

.soft-skills-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 2rem;
}

.soft-skill-item {
  background: rgba(255, 255, 255, 0.05);
  border-radius: 16px;
  padding: 2rem;
  border: 1px solid rgba(255, 255, 255, 0.1);
  transition: all 0.3s ease;
  text-align: center;
}

.soft-skill-item:hover {
  transform: translateY(-3px);
  background: rgba(255, 255, 255, 0.08);
}

.soft-skill-icon {
  width: 60px;
  height: 60px;
  background: linear-gradient(135deg, #667eea, #764ba2);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 0 auto 1rem;
}

.soft-skill-icon i {
  font-size: 1.5rem;
  color: white;
}

.soft-skill-content h4 {
  color: #ffffff;
  margin: 0 0 0.5rem 0;
  font-size: 1.1rem;
}

.soft-skill-content p {
  color: #a0a0a0;
  margin: 0;
  font-size: 0.9rem;
  line-height: 1.6;
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

.skill-particles {
  position: absolute;
  width: 100%;
  height: 100%;
}

.particle {
  position: absolute;
  width: 4px;
  height: 4px;
  background: #667eea;
  border-radius: 50%;
  animation: particleFloat 6s ease-in-out infinite;
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
.particle:nth-child(13) { top: 75%; left: 70%; animation-delay: 6s; }
.particle:nth-child(14) { top: 45%; right: 40%; animation-delay: 6.5s; }
.particle:nth-child(15) { top: 95%; left: 25%; animation-delay: 7s; }

@keyframes particleFloat {
  0%, 100% {
    transform: translateY(0px) scale(1);
    opacity: 0.3;
  }
  50% {
    transform: translateY(-20px) scale(1.2);
    opacity: 1;
  }
}

/* Responsive Design */
@media (max-width: 992px) {
  .skill-levels {
    grid-template-columns: 1fr;
  }
  
  .specialization-grid {
    grid-template-columns: 1fr;
  }
  

}

@media (max-width: 768px) {
  .level-card,
  .specialization-card,
  .learning-item,
  .soft-skill-item {
    padding: 1.5rem;
  }
  
  .soft-skills-grid {
    grid-template-columns: 1fr;
  }
}

@media (max-width: 576px) {
  .specialization-card,
  .spec-icon {
    margin: 0 auto 1rem;
  }
}
</style>