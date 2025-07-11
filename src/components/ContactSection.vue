<template>
  <section id="contact">
    <div class="container">
      <h2 class="section-title">Me <span>Contacter</span></h2>
      <p class="section-subtitle">Disponible pour des opportunités de stage</p>
      
      <div class="contact-container">
        <div class="contact-info">
          <h2>Mes coordonnées</h2>
          <div class="info-item" v-for="info in contactInfo" :key="info.text">
            <i :class="info.icon"></i>
            <span v-if="!info.isLink">{{ info.text }}</span>
            <a v-else :href="info.url" target="_blank">{{ info.text }}</a>
          </div>
          
          <div class="social-links">
            <a v-for="social in socialLinks" :key="social.icon" :href="social.url" target="_blank">
              <i :class="social.icon"></i>
            </a>
          </div>
        </div>
        
        <form @submit.prevent="submitForm" class="contact-form">
          <div class="form-group">
            <label for="name">Nom complet</label>
            <input type="text" id="name" v-model="form.name" required>
          </div>
          <div class="form-group">
            <label for="email">Email</label>
            <input type="email" id="email" v-model="form.email" required>
          </div>
          <div class="form-group">
            <label for="subject">Sujet</label>
            <input type="text" id="subject" v-model="form.subject" required>
          </div>
          <div class="form-group">
            <label for="message">Message</label>
            <textarea id="message" v-model="form.message" rows="5" required></textarea>
          </div>
          <button type="submit" class="btn btn-primary" :disabled="isSubmitting">
            <span v-if="!isSubmitting">Envoyer le message</span>
            <span v-else><i class="fas fa-spinner fa-spin"></i> Envoi en cours...</span>
          </button>
          
          <div v-if="submitMessage" class="alert" :class="{ success: isSuccess, error: !isSuccess }">
            <i :class="isSuccess ? 'fas fa-check-circle' : 'fas fa-exclamation-circle'"></i>
            <span>{{ submitMessage }}</span>
          </div>
        </form>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'ContactSection',
  data() {
    return {
      contactInfo: [
        { icon: 'fas fa-envelope', text: 'lanjaadrianjatovo@gmail.com', isLink: false },
        { icon: 'fas fa-phone', text: '+261 38 95 983 72', isLink: false },
        { icon: 'fas fa-phone', text: '+261 32 09 968 72', isLink: false },
        { icon: 'fas fa-map-marker-alt', text: 'Antananarivo, Madagascar', isLink: false },
        { icon: 'fab fa-github', text: 'github.com/lanjamrts', url: 'https://github.com/lanjamrts', isLink: true }
      ],
      socialLinks: [
        { icon: 'fab fa-github', url: 'https://github.com/lanjamrts' },
        { icon: 'fab fa-linkedin', url: '#' },
        { icon: 'fab fa-twitter', url: '#' },
        { icon: 'fas fa-envelope', url: 'mailto:lanjaadrianjatovo@gmail.com' }
      ],
      form: {
        name: '',
        email: '',
        subject: '',
        message: ''
      },
      isSubmitting: false,
      submitMessage: '',
      isSuccess: false
    }
  },
  methods: {
    submitForm() {
      this.isSubmitting = true
      
      // Simulation d'envoi (remplacer par un vrai appel API)
      setTimeout(() => {
        this.isSubmitting = false
        this.isSuccess = true
        this.submitMessage = 'Message envoyé avec succès ! Je vous répondrai dès que possible.'
        this.form = { name: '', email: '', subject: '', message: '' }
        
        // Effacer le message après 5 secondes
        setTimeout(() => {
          this.submitMessage = ''
        }, 5000)
      }, 1500)
    }
  }
}
</script>

<style scoped>
.contact-container {
  display: flex;
  gap: 3rem;
  margin-top: 3rem;
}

.contact-info {
  flex: 1;
  background-color: var(--dark-light);
  padding: 2rem;
  border-radius: 10px;
  border-left: 4px solid var(--primary);
}

.contact-info h2 {
  margin-bottom: 1.5rem;
  color: var(--primary);
}

.info-item {
  display: flex;
  align-items: center;
  gap: 1rem;
  margin-bottom: 1.5rem;
}

.info-item i {
  font-size: 1.2rem;
  color: var(--primary);
  width: 30px;
  text-align: center;
}

.info-item a {
  color: var(--light);
  text-decoration: none;
  transition: color 0.3s;
}

.info-item a:hover {
  color: var(--primary);
}

.social-links {
  display: flex;
  gap: 1.5rem;
  margin-top: 2rem;
}

.social-links a {
  color: var(--light);
  font-size: 1.5rem;
  transition: color 0.3s;
}

.social-links a:hover {
  color: var(--primary);
}

.contact-form {
  flex: 1;
}

.form-group {
  margin-bottom: 1.5rem;
}

.form-group label {
  display: block;
  margin-bottom: 0.5rem;
  font-weight: 500;
}

.form-group input,
.form-group textarea {
  width: 100%;
  padding: 0.8rem;
  background-color: var(--dark-light);
  border: 1px solid var(--secondary);
  border-radius: 5px;
  color: white;
  font-size: 1rem;
}

.form-group textarea {
  min-height: 150px;
  resize: vertical;
}

.alert {
  padding: 1rem;
  border-radius: 5px;
  margin-top: 1.5rem;
  display: flex;
  align-items: center;
  gap: 0.8rem;
}

.alert.success {
  background-color: rgba(0, 200, 83, 0.2);
  color: #00c853;
}

.alert.error {
  background-color: rgba(213, 0, 0, 0.2);
  color: #d50000;
}

@media (max-width: 768px) {
  .contact-container {
    flex-direction: column;
  }
}
</style>