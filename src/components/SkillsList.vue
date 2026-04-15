<template>
  <section id="skills" class="skills">
    <div class="container">
      <h2 class="section-title">Tech Stack</h2>
      <div class="skills-grid">
        <div v-for="skill in skills" :key="skill.name" class="skill-item nb-card">
          <div class="skill-icon">{{ skill.icon }}</div>
          <h3 class="skill-name">{{ skill.name }}</h3>
          <div class="skill-level">
            <div
              class="skill-bar"
              :style="{ width: skill.level + '%', background: skill.color }"
            ></div>
          </div>
          <p class="skill-desc">{{ skill.description }}</p>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref } from 'vue'

const skills = ref([
  {
    name: 'Vue / Nuxt',
    icon: '⚡',
    level: 95,
    color: 'var(--green)',
    description: 'Component architecture, Composition API, SSR'
  },
  {
    name: 'TypeScript',
    icon: '📘',
    level: 85,
    color: 'var(--cyan)',
    description: 'Type-safe development, interfaces, generics'
  },
  {
    name: 'CSS / SCSS',
    icon: '🎨',
    level: 90,
    color: 'var(--magenta)',
    description: 'Brutalist designs, animations, responsive'
  },
  {
    name: 'GSAP / Framer',
    icon: '🎬',
    level: 80,
    color: 'var(--yellow)',
    description: 'Scroll animations, micro-interactions'
  }
])
</script>

<style scoped>
.skills {
  padding: 80px 0;
}

.skills-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 24px;
}

.skill-item {
  padding: 24px;
}

.skill-icon {
  font-size: 2.5rem;
  margin-bottom: 16px;
}

.skill-name {
  font-size: 1.25rem;
  font-weight: 700;
  margin-bottom: 12px;
}

.skill-level {
  height: 12px;
  background: var(--bg);
  border: 2px solid var(--black);
  margin-bottom: 16px;
}

.skill-bar {
  height: 100%;
}

.skill-desc {
  font-size: 0.9rem;
  color: #555;
}

@media (max-width: 1024px) {
  .skills-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 640px) {
  .skills-grid {
    grid-template-columns: 1fr;
  }
}
</style>