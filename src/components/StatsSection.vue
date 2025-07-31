<template>
  <section class="stats">
    <div class="container">
      <div class="stat-item" v-for="stat in stats" :key="stat.value">
        <h3>{{ stat.value }}</h3>
        <p>{{ stat.label }}</p>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'StatsSection',
  data() {
    return {
      stats: [
        { value: '2+', label: 'Années d\'expérience académique' },
        { value: '15+', label: 'Projets réalisés' },
        { value: '5+', label: 'Technologies maîtrisées' },
        { value: '100%', label: 'Engagement' }
      ]
    }
  }
}
</script>

<style scoped>
.stats {
  background-color: #0a192f;
  padding: 3rem 0;
}

.stats .container {
  display: flex;
  justify-content: space-around;
  flex-wrap: wrap;
  gap: 2rem;
}

.stat-item {
  text-align: center;
  padding: 1.5rem;
  min-width: 150px;
  border: 1px solid #233554;
  border-radius: 8px;
  background: #112240;
}

.stat-item h3 {
  font-size: 2.5rem;
  color: #e6f1ff;
  margin-bottom: 0.5rem;
}

.stat-item p {
  color: #8892b0;
  font-size: 1rem;
}

@media (max-width: 576px) {
  .stats .container {
    flex-direction: column;
    align-items: center;
  }
}
</style>