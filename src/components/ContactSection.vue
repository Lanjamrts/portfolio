<template>
  <section id="contact">
    <div class="container">
      <h2 class="section-title">Me <span>Contacter</span></h2>
      <p class="section-subtitle">N'hésitez pas à me contacter directement par email, téléphone ou Facebook :</p>
      <div class="contact-simple">
        <div class="contact-item">
          <i class="fas fa-envelope"></i>
          <a href="mailto:lanjaandrianjatovo@gmail.com">lanjaandrianjatovo@gmail.com</a>
        </div>
        <div class="contact-item">
          <i class="fas fa-phone"></i>
          <span>+261 38 95 983 72</span>
        </div>
        <div class="contact-item">
          <i class="fas fa-phone"></i>
          <span>+261 32 09 968 72</span>
        </div>
        <div class="contact-item">
          <i class="fab fa-facebook"></i>
          <a href="https://www.facebook.com/lanja.mirantsoa.37/" target="_blank">lanja Andrianjatovo</a>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'ContactSection'
}
</script>

<style scoped>
.contact-simple {
  display: flex;
  flex-direction: column;
  gap: 2rem;
  margin: 3rem auto 0 auto;
  max-width: 500px;
  background: #1a1a1a;
  border-radius: 12px;
  box-shadow: 0 4px 24px rgba(0,0,0,0.18);
  padding: 2.5rem 2rem;
}

.contact-item {
  display: flex;
  align-items: center;
  gap: 1.2rem;
  font-size: 1.2rem;
  color: #ffffff;
}

.contact-item i {
  font-size: 1.5rem;
  min-width: 32px;
  text-align: center;
}

.contact-item .fa-envelope {
  color: #EA4335;
}
.contact-item .fa-phone {
  color: #34A853;
}
.contact-item .fa-facebook {
  color: #1877F3;
}

.contact-item a {
  color: #7f9cf5;
  text-decoration: none;
  font-weight: 500;
  transition: color 0.2s;
}

.contact-item a:hover {
  color: #b3c7fa;
  text-decoration: underline;
}
.contact-item a,
.contact-item span {
  word-break: break-word;
  overflow-wrap: break-word;
  max-width: 100%;
  display: inline-block;
}
@media (max-width: 480px) {
  .contact-simple {
    padding: 2rem 1rem;
  }

  .contact-item {
    font-size: 1rem;
    flex-direction: column;
    align-items: flex-start;
    gap: 0.5rem;
  }

  .contact-item i {
    font-size: 1.3rem;
  }
}

</style>