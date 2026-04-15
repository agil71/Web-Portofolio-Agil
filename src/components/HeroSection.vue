<template>
  <section class="hero">
    <div class="container">
      <div class="hero-grid">
        <div class="hero-content">
          <span class="badge" @click="toggleAvailable">
            <span class="badge-dot" :class="{ 'active': isAvailable }"></span>
            {{ isAvailable ? '✨ Available for work' : '🔴 Currently Busy' }}
          </span>
          <h1 class="hero-title">
            Building
            <span class="highlight" @click="changeWord">
              {{ currentWord }}
            </span>
            experiences with
            <span class="highlight-alt">brutal</span>
            honesty.
          </h1>
          <p class="hero-description">
            Hello! I'm Agil. Student of Mulawarman University & UI enthusiast. I craft bold, accessible web applications that are not afraid to make a statement.
          </p>
          
          <div class="hero-actions">
            <a href="#work" class="nb-button primary-btn" @click.prevent="smoothScroll('#work')">
              <span>View Work</span>
              <span class="btn-arrow">→</span>
              <div class="btn-shine"></div>
            </a>
            
            <!-- CONTACT BUTTON -->
            <button class="nb-button secondary-btn" @click="handleContact">
              <span>Contact</span>
              <span class="btn-arrow">↗</span>
            </button>
          </div>
          
          <div class="hero-stats">
            <div class="stat-item" v-for="stat in stats" :key="stat.label">
              <span class="stat-number">{{ stat.displayValue }}</span>
              <span class="stat-label">{{ stat.label }}</span>
            </div>
          </div>
        </div>
        <div class="hero-visual">
          <div class="nb-card avatar-card">
            <div class="avatar-container">
              <img src="/me.jpeg" alt="Agil Aji Munawar" class="profile-photo" />
            </div>
            <div class="stats">
              <div class="stat">
                <span class="stat-number">{{ animatedExp }}</span>
                <span class="stat-label">Years Exp</span>
              </div>
              <div class="stat">
                <span class="stat-number">{{ animatedProjects }}</span>
                <span class="stat-label">Projects</span>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const emit = defineEmits(['open-contact'])

const words = ['digital', 'bold', 'unique', 'raw', 'honest']
const currentWord = ref('digital')
const wordIndex = ref(0)
const isAvailable = ref(true)
const animatedExp = ref(0)
const animatedProjects = ref(0)

const stats = ref([
  { label: 'Years Experience', value: 4, displayValue: 0 },
  { label: 'Projects Done', value: 10, displayValue: 0 },
  { label: 'Happy Clients', value: 12, displayValue: 0 }
])

const toggleAvailable = () => {
  isAvailable.value = !isAvailable.value
}

const changeWord = () => {
  wordIndex.value = (wordIndex.value + 1) % words.length
  currentWord.value = words[wordIndex.value]
}

const smoothScroll = (selector) => {
  const element = document.querySelector(selector)
  if (element) {
    element.scrollIntoView({ behavior: 'smooth' })
  }
}

const handleContact = () => {
  console.log('Contact button clicked!') // Debug
  emit('open-contact')
}

const animateNumbers = () => {
  const duration = 2000
  const steps = 60
  const interval = duration / steps
  
  let step = 0
  const timer = setInterval(() => {
    step++
    const progress = step / steps
    
    stats.value[0].displayValue = Math.floor(4 * progress)
    stats.value[1].displayValue = Math.floor(10 * progress)
    stats.value[2].displayValue = Math.floor(12 * progress)
    animatedExp.value = Math.floor(5 * progress)
    animatedProjects.value = Math.floor(10 * progress)
    
    if (step >= steps) {
      clearInterval(timer)
      stats.value[0].displayValue = 4
      stats.value[1].displayValue = 10
      stats.value[2].displayValue = 12
      animatedExp.value = 4
      animatedProjects.value = 10
    }
  }, interval)
}

onMounted(() => {
  animateNumbers()
  
  setInterval(() => {
    changeWord()
  }, 3000)
})
</script>

<style scoped>
.hero {
  padding: 80px 0;
}

.hero-grid {
  display: grid;
  grid-template-columns: 1.5fr 1fr;
  gap: 60px;
  align-items: center;
}

.badge {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  padding: 8px 20px;
  background: var(--cyan);
  border: 3px solid var(--black);
  font-weight: 600;
  margin-bottom: 24px;
  cursor: pointer;
  transition: all 0.2s;
}

.badge:hover {
  transform: translate(-2px, -2px);
  box-shadow: 4px 4px 0 var(--black);
}

.badge-dot {
  width: 10px;
  height: 10px;
  border-radius: 50%;
  background: #ff4444;
  transition: all 0.3s;
}

.badge-dot.active {
  background: #00ff88;
}

.hero-title {
  font-size: clamp(2.5rem, 6vw, 4.5rem);
  font-weight: 700;
  line-height: 1.1;
  letter-spacing: -0.03em;
  margin-bottom: 24px;
}

.highlight {
  background: var(--yellow);
  padding: 0 8px;
  display: inline-block;
  border: 3px solid var(--black);
  cursor: pointer;
  transition: all 0.2s;
}

.highlight:hover {
  transform: scale(1.05) rotate(-2deg);
  box-shadow: 4px 4px 0 var(--black);
}

.highlight-alt {
  background: var(--magenta);
  color: var(--white);
  padding: 0 8px;
  display: inline-block;
  border: 3px solid var(--black);
}

.hero-description {
  font-size: 1.25rem;
  margin-bottom: 32px;
  max-width: 500px;
  line-height: 1.6;
}

.hero-actions {
  display: flex;
  gap: 16px;
  margin-bottom: 48px;
}

.nb-button {
  display: inline-flex;
  align-items: center;
  gap: 0.6rem;
  background: var(--yellow);
  border: 3px solid var(--black);
  box-shadow: 8px 8px 0 var(--black);
  font-weight: 700;
  text-transform: uppercase;
  text-decoration: none;
  color: var(--black);
  cursor: pointer;
  padding: 12px 24px;
  transition: all 0.1s ease;
  font-size: 1rem;
}

.nb-button:hover {
  transform: translate(4px, 4px);
  box-shadow: 4px 4px 0 var(--black);
}

.primary-btn {
  position: relative;
  overflow: hidden;
}

.btn-shine {
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: linear-gradient(90deg, transparent, rgba(255,255,255,0.3), transparent);
  transition: left 0.5s;
}

.primary-btn:hover .btn-shine {
  left: 100%;
}

.btn-arrow {
  margin-left: 8px;
  transition: transform 0.3s;
  display: inline-block;
}

.nb-button:hover .btn-arrow {
  transform: translateX(4px);
}

.secondary-btn {
  background: var(--white) !important;
}

.hero-stats {
  display: flex;
  gap: 40px;
}

.stat-item {
  display: flex;
  flex-direction: column;
}

.stat-number {
  font-size: 2.5rem;
  font-weight: 700;
}

.avatar-card {
  padding: 32px;
  text-align: center;
}

.avatar-container {
  width: 100%;
  aspect-ratio: 1;
  margin-bottom: 24px;
  border: var(--border);
  overflow: hidden;
}

.profile-photo {
  width: 100%;
  height: 100%;
  object-fit: cover;
  display: block;
}

.stats {
  display: flex;
  justify-content: space-around;
  gap: 20px;
}

.stat {
  display: flex;
  flex-direction: column;
}

@media (max-width: 768px) {
  .hero-grid {
    grid-template-columns: 1fr;
    gap: 40px;
  }
  
  .hero-actions {
    flex-direction: column;
  }
  
  .nb-button {
    text-align: center;
    justify-content: center;
  }
  
  .hero-stats {
    justify-content: space-between;
  }
}
</style>