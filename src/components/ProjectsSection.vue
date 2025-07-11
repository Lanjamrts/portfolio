<template>
  <section id="projects">
    <div class="container">
      <h2 class="section-title">Mes <span>Projets</span></h2>
      <p class="section-subtitle">Découvrez une sélection de mes réalisations</p>
      
      <div class="projects-filter">
        <button 
          v-for="filter in filters" 
          :key="filter.value"
          @click="activeFilter = filter.value"
          :class="{ active: activeFilter === filter.value }"
          class="filter-btn"
        >
          {{ filter.label }}
        </button>
      </div>
      
      <div class="projects-grid">
        <div 
          class="project-card" 
          v-for="project in filteredProjects" 
          :key="project.id"
          :data-category="project.category"
        >
          <div class="project-image">
            <img :src="project.image" :alt="project.title">
            <div class="project-links">
              <a :href="project.demoUrl" class="link-icon"><i class="fas fa-link"></i></a>
              <a :href="project.githubUrl" class="link-icon"><i class="fab fa-github"></i></a>
            </div>
          </div>
          <div class="project-info">
            <h3>{{ project.title }}</h3>
            <p>{{ project.description }}</p>
            <div class="project-tech">
              <span v-for="tech in project.technologies" :key="tech">{{ tech }}</span>
            </div>
          </div>
        </div>
      </div>

    </div>
  </section>
</template>

<script>
export default {
  name: 'ProjectsSection',
  data() {
    return {
      activeFilter: 'all',
      filters: [
        { value: 'all', label: 'Tous' },
        { value: 'web', label: 'Web' },
        { value: 'mobile', label: 'Mobile' },
        { value: 'academic', label: 'Académiques' }
      ],
      projects: [
        {
          id: 1,
          title: 'Site E-commerce',
          description: 'Site de commerce électronique, spécialisé dans la vente de ordinateur ',
          category: 'web',
          technologies: ['.Net'],
          image: require('@/assets/images/e-commerce.png'),
          demoUrl: '#',
          githubUrl: '#'
        },
        {
          id: 2,
          title: 'Application météo',
          description: 'un site fournissant des prévisions en temps réel, développé avec Angular et intégrant une API.',
          category: 'academic',
          technologies: ['Angular'],
          image: require('@/assets/images/la-meteo.png'),
          demoUrl: '#',
          githubUrl: '#'
        },
        {
          id: 3,
          title: 'Microservice',
          description: 'un site web conçu selon une architecture de microservices, développé avec Docker. Les détails spécifiques de son contenu ne sont plus disponibles.',
          category: 'web',
          technologies: ['Docker'],
                    image: require('@/assets/images/microservice.png'),
          demoUrl: '#',
          githubUrl: '#'
        },
      ]
    }
  },
  computed: {
    filteredProjects() {
      if (this.activeFilter === 'all') {
        return this.projects
      }
      return this.projects.filter(project => project.category === this.activeFilter)
    }
  }
}
</script>

<style scoped>
.projects-filter {
  display: flex;
  justify-content: center;
  gap: 1rem;
  margin-bottom: 2rem;
  flex-wrap: wrap;
}

.filter-btn {
  background: none;
  border: 1px solid var(--primary);
  color: var(--primary);
  padding: 0.5rem 1.5rem;
  border-radius: 50px;
  cursor: pointer;
  transition: all 0.3s;
}

.filter-btn.active, .filter-btn:hover {
  background-color: var(--primary);
  color: white;
}

.projects-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(350px, 1fr));
  gap: 2rem;
  margin-top: 2rem;
}

.project-card {
  background-color: var(--dark-light);
  border-radius: 10px;
  overflow: hidden;
  transition: transform 0.3s, box-shadow 0.3s;
}

.project-card:hover {
  transform: translateY(-10px);
  box-shadow: 0 15px 30px rgba(0, 0, 0, 0.2);
}

.project-image {
  position: relative;
  height: 200px;
  overflow: hidden;
}

.project-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.5s;
}

.project-card:hover .project-image img {
  transform: scale(1.1);
}

.project-links {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.7);
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 1.5rem;
  opacity: 0;
  transition: opacity 0.3s;
}

.project-card:hover .project-links {
  opacity: 1;
}

.link-icon {
  color: white;
  font-size: 1.5rem;
  width: 50px;
  height: 50px;
  border-radius: 50%;
  background-color: var(--primary);
  display: flex;
  justify-content: center;
  align-items: center;
  transition: transform 0.3s;
}

.link-icon:hover {
  transform: scale(1.2);
}

.project-info {
  padding: 1.5rem;
}

.project-info h3 {
  margin-bottom: 0.5rem;
}

.project-info p {
  color: var(--gray);
  margin-bottom: 1rem;
}

.project-tech {
  display: flex;
  gap: 0.7rem;
  flex-wrap: wrap;
}

.project-tech span {
  background-color: rgba(41, 98, 255, 0.2);
  color: var(--primary);
  padding: 0.3rem 0.8rem;
  border-radius: 50px;
  font-size: 0.8rem;
}

.github-cta {
  text-align: center;
  margin-top: 4rem;
}

@media (max-width: 400px) {
  .projects-grid {
    grid-template-columns: 1fr;
  }
}
</style>