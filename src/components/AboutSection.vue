<template>
  <section id="about">
    <div class="container">
      <h2 class="section-title">À <span>propos</span></h2>
      <p class="section-subtitle">Apprenez à me connaître</p>
      
      <div class="about-content">
        <div class="about-text">
          <h3>Je suis Adrianjatovo Lanja, étudiant en Génie Logiciel</h3>
          <p>Actuellement étudiant 2ème Année à l'INSI Ambanidia, je me spécialise dans le développement web et logiciel. Passionné par les nouvelles technologies, j'aime créer des solutions innovantes et fonctionnelles.</p>
          
          <div class="about-details">
            <div class="detail-item">
              <span><strong>Nom :</strong> Adrianjatovo Lanja</span>
              <span><strong>Email :</strong> lanjaadrianjatovo@gmail.com</span>
            </div>
            <div class="detail-item">
              <span><strong>Téléphone :</strong> +261 38 95 983 72</span>
              <span><strong>Ville :</strong> Antananarivo, Madagascar</span>
            </div>
          </div>
          
          <p>Je recherche activement un stage pour mettre en pratique mes connaissances et développer de nouvelles compétences dans un environnement professionnel.</p>
        </div>
        <div class="about-image">
          <img src="@/assets/images/profile.png" alt="Adrianjatovo Lanja">
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'AboutSection',
  mounted() {
    const elements = document.querySelectorAll(
      '.about-text h3, .about-text p, .about-details, .about-image img'
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
}
</script>


<style scoped>
/* Animations */
@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(30px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@keyframes scaleIn {
  from {
    opacity: 0;
    transform: scale(0.9);
  }
  to {
    opacity: 1;
    transform: scale(1);
  }
}

/* Animation appliquée aux éléments */
.about-text h3,
.about-text p,
.about-details,
.about-image img {
  opacity: 0;
  animation: fadeInUp 0.8s ease forwards;
  animation-play-state: paused;
}

.about-text h3 { animation-delay: 0.2s; }
.about-text p:first-of-type { animation-delay: 0.4s; }
.about-details { animation-delay: 0.6s; }
.about-text p:last-of-type { animation-delay: 0.8s; }
.about-image img {
  animation: scaleIn 1s ease forwards;
  animation-delay: 0.5s;
  transition: transform 0.3s ease;
}

/* Hover effet sur image */
.about-image img:hover {
  transform: scale(1.05);
  box-shadow: 0 10px 25px rgba(0, 0, 0, 0.3);
}
</style>
