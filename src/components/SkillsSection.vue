<template>
  <section id="skills">
    <div class="container">
      <h2 class="section-title">Mes <span>Compétences</span></h2>
      <p class="section-subtitle">Technologies que je maîtrise</p>

      <div class="skills-categories">
        <div class="category-card" v-for="category in skillCategories" :key="category.name">
          <div class="category-header">
            <i :class="category.icon"></i>
            <h2>{{ category.name }}</h2>
          </div>
          <div class="skills-list">
            <div class="skill-item" v-for="skill in category.skills" :key="skill.name">
              <div class="skill-info">
                <span>{{ skill.name }}</span>
                <span>{{ skill.percentage }}%</span>
              </div>
              <div class="progress-bar">
                <div class="progress" :style="{ width: skill.percentage + '%' }"></div>
              </div>
            </div>
          </div>
        </div>
      </div>

      <div class="additional-skills">
        <h2>Autres Compétences</h2>
        <div class="skills-tags">
          <span class="tag" v-for="skill in otherSkills" :key="skill">{{ skill }}</span>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
  export default {
    name: 'SkillsSection',
    data() {
      return {
        skillCategories: [{
            name: 'Frontend',
            icon: 'fas fa-laptop-code',
            skills: [{
                name: 'HTML5',
                percentage: 85
              },
              {
                name: 'CSS3',
                percentage: 80
              },
              {
                name: 'JavaScript',
                percentage: 70
              },
              {
                name: 'Bootstrap',
                percentage: 65
              }
            ]
          },
          {
            name: 'Backend',
            icon: 'fas fa-server',
            skills: [{
                name: 'PHP',
                percentage: 60
              },
              {
                name: 'MySQL',
                percentage: 60
              },
              {
                name: '.NET',
                percentage: 45
              }
            ]
          },
          {
            name: 'Frameworks',
            icon: 'fas fa-layer-group',
            skills: [{
                name: 'Angular',
                percentage: 55
              },
              {
                name: 'Sass',
                percentage: 50
              },
              {
                name: 'Vue.js',
                percentage: 45
              }

            ]
          },
          {
            name: 'Outils',
            icon: 'fas fa-tools',
            skills: [{

                name: 'VS Code',
                percentage: 85
              },
              {

                name: 'Docker',
                percentage: 75
              },
              {
                name: 'Git/GitHub',
                percentage: 60
              } // Ajout de Docker avec un pourcentage
            ]
          }
        ],
        otherSkills: [
          'Responsive Design',
          'Base de données',
          'Résolution de problèmes',
          'Travail d\'équipe'
        ]
      }
    },
    mounted() {
      this.animateSkills()
    },
    methods: {
      animateSkills() {
        const skills = document.querySelectorAll('.progress')
        skills.forEach(skill => {
          const width = skill.style.width
          skill.style.width = '0'
          setTimeout(() => {
            skill.style.width = width
          }, 100)
        })
      }
    }
  }
</script>

<style scoped>
  /* Vos styles CSS pour la section Compétences */
  .skills-categories {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 2rem;
  }

  .category-card {
    background-color: var(--dark-light);
    border-radius: 10px;
    padding: 2rem;
  }

  /* ... autres styles ... */
</style>