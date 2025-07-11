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
  background-color: var(--dark-light);
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
}

.stat-item h3 {
  font-size: 2.5rem;
  color: var(--primary);
  margin-bottom: 0.5rem;
}

@media (max-width: 576px) {
  .stats .container {
    flex-direction: column;
    align-items: center;
  }
}
</style>