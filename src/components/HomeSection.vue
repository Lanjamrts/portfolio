<template>
  <section id="home" class="home-section">
    <div class="container">
      <div class="hero">
        <div class="hero-content">
          <h2 class="typewriter">{{ typewriterText }}</h2>
          <div class="hero-text">
            <p class="hero-description">
              Passionné par le développement web et les technologies modernes, 
              je recherche un stage pour appliquer mes compétences et contribuer 
              à des projets innovants.
            </p>
          </div>
          <div class="hero-cta">
            <a href="#contact" class="btn btn-primary">
              <span>Me contacter</span>
              <i class="fas fa-arrow-right"></i>
            </a>
            <a href="/cv-lanja.pdf" class="btn btn-secondary">
              <i class="fas fa-download"></i>
              <span>Voir mon CV</span>
            </a>
          </div>
          <div class="social-links">
            <a 
              v-for="social in socialLinks" 
              :key="social.id" 
              :href="social.url" 
              :target="social.target"
              :class="`social-link ${social.class}`"
              :title="social.title"
            >
              <i :class="social.icon"></i>
            </a>
          </div>
        </div>
        <div class="hero-profile">
          <div class="profile-container">
            <img src="@/assets/images/profile.png" alt="Adrianjatovo Lanja" class="profile-img">
          </div>
          <div class="profile-name">Adrianjatovo Lanja</div>
        </div>
      </div>
    </div>
    <!-- Background decoration -->
    <div class="bg-decoration">
      <div class="floating-shape shape-1"></div>
      <div class="floating-shape shape-2"></div>
      <div class="floating-shape shape-3"></div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'HomeSection',
  data() {
    return {
      socialLinks: [
        { id: 1, url: 'https://github.com/lanjamrts', target: '_blank', icon: 'fab fa-github', title: 'GitHub', class: 'github' },
        { id: 2, url: 'https://www.linkedin.com/in/lanja-mirantsoa-90273a374?utm_source=share&utm_campaign=share_via&utm_content=profile&utm_medium=android_app', target: '_blank', icon: 'fab fa-linkedin', title: 'LinkedIn', class: 'linkedin' },
        { id: 3, url: 'mailto:lanjaandrianjatovo@gmail.com', target: '', icon: 'fas fa-envelope', title: 'Email', class: 'email' }
      ],
      typewriterText: '',
      fullText: 'Développeur Web',
      typewriterIndex: 0,
      typing: true
    };
  },
  mounted() {
    this.initAnimations();
    this.startTypewriter();
  },
  methods: {
    initAnimations() {
      const elements = document.querySelectorAll(
        '.typewriter, .hero-description, .hero-cta, .social-links, .hero-profile'
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
    },
    startTypewriter() {
      this.typewriterText = '';
      this.typewriterIndex = 0;
      this.typing = true;
      this.typeLetter();
    },
    typeLetter() {
      if (this.typewriterIndex < this.fullText.length) {
        this.typewriterText += this.fullText[this.typewriterIndex];
        this.typewriterIndex++;
        setTimeout(this.typeLetter, 120);
      } else {
        this.typing = false;
        setTimeout(this.eraseText, 1200);
      }
    },
    eraseText() {
      if (this.typewriterIndex > 0) {
        this.typewriterText = this.typewriterText.slice(0, -1);
        this.typewriterIndex--;
        setTimeout(this.eraseText, 60);
      } else {
        this.typing = true;
        setTimeout(this.typeLetter, 400);
      }
    }
  }
};
</script>

<style scoped>
.home-section {
  min-height: 100vh;
  display: flex;
  align-items: center;
  padding-top: 80px;
  position: relative;
  overflow: hidden;
  background: linear-gradient(135deg, #0a0a0a 0%, #18141c 100%);
}
.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 2rem;
}
.hero {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 4rem;
  position: relative;
  z-index: 2;
}
.hero-content {
  flex: 1;
  max-width: 600px;
  display: flex;
  flex-direction: column;
  align-items: center;
}
.hero-profile {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: flex-start;
  min-width: 220px;
}
.profile-container {
  display: flex;
  justify-content: center;
  align-items: center;
}
.profile-img {
  width: 180px;
  height: 180px;
  border-radius: 50%;
  object-fit: cover;
  border: 4px solid #233554;
  box-shadow: 0 4px 24px rgba(100,255,218,0.08);
}
.profile-name {
  text-align: center;
  color: #e6f1ff;
  font-size: 2.2rem;
  font-weight: 700;
  margin-top: 1.5rem;
  letter-spacing: 2px;
}
.typewriter {
  font-size: 3.2rem;
  font-weight: 700;
  text-align: center;
  background: linear-gradient(270deg, #64ffda, #233554, #e6f1ff, #64ffda);
  background-size: 800% 800%;
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  animation: gradientMove 4s ease-in-out infinite;
  margin-bottom: 1.2rem;
  letter-spacing: 2px;
  min-height: 3.5rem;
  white-space: nowrap;
  border-right: 2px solid #64ffda;
  overflow: hidden;
}
@keyframes gradientMove {
  0% { background-position: 0% 50%; }
  50% { background-position: 100% 50%; }
  100% { background-position: 0% 50%; }
}
.hero-description {
  font-size: 1.2rem;
  color: #8892b0;
  margin-bottom: 2rem;
  text-align: center;
}
.hero-cta {
  display: flex;
  gap: 1rem;
  justify-content: center;
  margin-bottom: 2rem;
}
.social-links {
  display: flex;
  gap: 1rem;
  justify-content: center;
}
@media (max-width: 992px) {
  .hero {
    flex-direction: column;
    gap: 2.5rem;
  }
  .hero-content {
    max-width: 100%;
  }
  .hero-profile {
    min-width: 0;
  }
}
</style>
