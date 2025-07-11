<template>
  <section id="home">
    <div class="container">
      <div class="hero">
        <div class="hero-content">
          <h1>Adrianjatovo <span>Lanja</span></h1>
          <h2>Étudiant en Génie Logiciel</h2>
          <p>Passionné par le développement web, je recherche un stage pour appliquer mes compétences.</p>

          <div class="hero-cta">
            <a href="#contact" class="btn btn-primary">Me contacter <i class="fas fa-arrow-right"></i></a>
            <!-- ✅ Téléchargement direct -->
            <a href="/cv-lanja.pdf" download class="btn btn-secondary">
              Télécharger mon CV
            </a>
          </div>

          <div class="social-links">
            <a v-for="social in socialLinks" :key="social.id" :href="social.url" :target="social.target">
              <i :class="social.icon"></i>
            </a>
          </div>
        </div>
        <div class="hero-image">
          <img src="@/assets/images/profile.png" alt="Adrianjatovo Lanja" class="profile-img">
          <div class="tech-icons">
            <i v-for="tech in technologies" :key="tech.name" :class="tech.icon" :title="tech.name"></i>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'HomeSection',
  data() {
    return {
      socialLinks: [
        { id: 1, url: 'https://github.com/lanjamrts', target: '_blank', icon: 'fab fa-github' },
        { id: 2, url: '#', target: '', icon: 'fab fa-linkedin' },
        { id: 3, url: 'mailto:lanjaandrianjatovo@gmail.com', target: '', icon: 'fas fa-envelope' }
      ],
      technologies: [
        { name: 'HTML5', icon: 'fab fa-html5' },
        { name: 'CSS3', icon: 'fab fa-css3-alt' },
        { name: 'JavaScript', icon: 'fab fa-js' },
        { name: 'Angular', icon: 'fab fa-angular' },
        { name: 'Vue.js', icon: 'fab fa-vuejs' },
        { name: 'PHP', icon: 'fab fa-php' }
      ]
    };
  },
  mounted() {
    const elements = document.querySelectorAll(
      '.hero-content h1, .hero-content h2, .hero-content p, .hero-cta, .social-links, .hero-image img, .tech-icons'
    );

    elements.forEach(el => {
      el.style.animationPlayState = 'paused';
    });

    const observer = new IntersectionObserver((entries) => {
      entries.forEach(entry => {
        if (entry.isIntersecting) {
          entry.target.style.animationPlayState = 'running';
          observer.unobserve(entry.target);
        }
      });
    }, { threshold: 0.2 });

    elements.forEach(el => observer.observe(el));
  }
};
</script>
