<template>
  <section id="work" class="work">
    <div class="container">
      <div class="section-header">
        <h2 class="section-title">
          <span class="title-text">Selected Work</span>
          <span class="title-decoration"></span>
        </h2>
        <div class="filter-controls">
          <button 
            v-for="tag in allTags" 
            :key="tag"
            @click="toggleFilter(tag)"
            :class="{ 'active': activeFilters.includes(tag) }"
            class="filter-btn"
          >
            {{ tag }}
          </button>
          <button @click="clearFilters" class="filter-btn clear-btn">
            Clear
          </button>
        </div>
      </div>
      
      <transition-group name="grid" tag="div" class="work-grid">
        <ProjectCard
          v-for="project in filteredProjects"
          :key="project.id"
          :project="project"
          @filter-tag="handleTagFilter"
          @view-project="handleViewProject"
        />
      </transition-group>
      
      <div class="load-more" v-if="hasMoreProjects">
        <button @click="loadMore" class="nb-button load-more-btn">
          <span>Load More</span>
          <span class="loading-dots" v-if="isLoading">
            <span>.</span><span>.</span><span>.</span>
          </span>
        </button>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, computed } from 'vue'
import ProjectCard from './ProjectCard.vue'

const allProjects = ref([
  {
    id: 1,
    title: 'PETSHOP WEB',
    category: 'Web Development',
    description: 'Website yang menjual semua kebutuhan hewan peliharaan.',
    image: '/projects/project1.jpeg',
    emoji: '🐾',
    color: '#00e5ff',
    tags: ['HTML', 'CSS', 'JS', 'PHP'],
    detail: 'Website e-commerce untuk petshop dengan fitur katalog produk, keranjang belanja, dan sistem pembayaran online.',
    timeline: '2 months',
    role: 'Full Stack Developer'
  },
  {
    id: 2,
    title: 'VENDING MACHINE APP',
    category: 'Desktop Application',
    description: 'Aplikasi simulasi Vending Machine.',
    image: '/projects/project2.jpeg',
    emoji: '🤖',
    color: '#ff007f',
    tags: ['JAVA'],
    detail: 'Aplikasi desktop simulasi vending machine dengan GUI interaktif dan sistem transaksi lengkap.',
    timeline: '1 month',
    role: 'Java Developer'
  },
  {
    id: 3,
    title: 'CLASSIFICATION UKT APP',
    category: 'Mobile Application',
    description: 'Aplikasi untuk mengklasifikasikan UKT Mahasiswa.',
    image: '/projects/project4.jpeg',
    emoji: '📱',
    color: '#00ff88',
    tags: ['DART', 'Flutter'],
    detail: 'Aplikasi mobile untuk klasifikasi UKT menggunakan algoritma Naive Bayes dengan akurasi tinggi.',
    timeline: '1 month',
    role: 'Mobile Developer'
  },
  {
    id: 4,
    title: 'PETSHOP WEB',
    category: 'Web Development',
    description: 'Website yang menjual semua kebutuhan hewan peliharaan.',
    image: '/projects/project3.jpeg',
    emoji: '🎯',
    color: '#ffdd00',
    tags: ['HTML', 'JS', 'CSS', 'PHP'],
    detail: 'Website e-commerce untuk petshop dengan fitur katalog produk, keranjang belanja, dan sistem pembayaran online.',
    timeline: '1 month',
    role: 'Frontend Developer'
  },
//   {
//     id: 5,
//     title: 'CRYPT0 DASH',
//     category: 'Web3 Dashboard',
//     description: 'Real-time crypto portfolio tracker.',
//     image: '/projects/crypto.jpg',
//     emoji: '🪙',
//     color: '#00e5ff',
//     tags: ['Vue', 'D3', 'WebSocket'],
//     detail: 'Dashboard cryptocurrency real-time dengan visualisasi data dan portfolio tracking.',
//     timeline: '2 months',
//     role: 'Lead Developer'
//   },
//   {
//     id: 6,
//     title: 'NEON ARCHIVE',
//     category: 'E-commerce',
//     description: 'Streetwear brand e-commerce platform.',
//     image: '/projects/neon.jpg',
//     emoji: '👕',
//     color: '#ff007f',
//     tags: ['Nuxt', 'Shopify', 'GSAP'],
//     detail: 'Platform e-commerce untuk brand streetwear dengan desain bold dan animasi halus.',
//     timeline: '4 months',
//     role: 'Frontend Developer'
//   }
])

const activeFilters = ref([])
const visibleCount = ref(4)
const isLoading = ref(false)

const allTags = computed(() => {
  const tags = new Set()
  allProjects.value.forEach(project => {
    project.tags.forEach(tag => tags.add(tag))
  })
  return Array.from(tags)
})

const filteredProjects = computed(() => {
  let filtered = allProjects.value
  
  if (activeFilters.value.length > 0) {
    filtered = filtered.filter(project =>
      activeFilters.value.some(filter => project.tags.includes(filter))
    )
  }
  
  return filtered.slice(0, visibleCount.value)
})

const hasMoreProjects = computed(() => {
  const filtered = activeFilters.value.length > 0
    ? allProjects.value.filter(project =>
        activeFilters.value.some(filter => project.tags.includes(filter))
      )
    : allProjects.value
    
  return visibleCount.value < filtered.length
})

const toggleFilter = (tag) => {
  const index = activeFilters.value.indexOf(tag)
  if (index > -1) {
    activeFilters.value.splice(index, 1)
  } else {
    activeFilters.value.push(tag)
  }
  visibleCount.value = 4
}

const clearFilters = () => {
  activeFilters.value = []
  visibleCount.value = 4
}

const handleTagFilter = (tag) => {
  if (!activeFilters.value.includes(tag)) {
    activeFilters.value.push(tag)
    visibleCount.value = 4
  }
}

const loadMore = () => {
  isLoading.value = true
  setTimeout(() => {
    visibleCount.value += 4
    isLoading.value = false
  }, 500)
}

const handleViewProject = (project) => {
  console.log('View project:', project)
  alert(`Viewing: ${project.title}\n\n${project.detail}`)
}
</script>

<style scoped>
.work {
  padding: 80px 0;
  background: var(--white);
  border-top: var(--border);
  border-bottom: var(--border);
}

.section-header {
  margin-bottom: 48px;
}

.section-title {
  font-size: clamp(2.5rem, 8vw, 4rem);
  font-weight: 700;
  margin-bottom: 24px;
  text-transform: uppercase;
  letter-spacing: -0.02em;
  display: flex;
  align-items: center;
  gap: 20px;
}

.title-decoration {
  flex: 1;
  height: 4px;
  background: repeating-linear-gradient(90deg, var(--black), var(--black) 10px, transparent 10px, transparent 20px);
}

.filter-controls {
  display: flex;
  flex-wrap: wrap;
  gap: 12px;
  margin-top: 20px;
}

.filter-btn {
  padding: 8px 16px;
  background: var(--white);
  border: 2px solid var(--black);
  font-weight: 600;
  text-transform: uppercase;
  font-size: 0.8rem;
  cursor: pointer;
  transition: all 0.2s;
}

.filter-btn:hover {
  transform: translate(-2px, -2px);
  box-shadow: 4px 4px 0 var(--black);
}

.filter-btn.active {
  background: var(--yellow);
  box-shadow: 4px 4px 0 var(--black);
}

.clear-btn {
  background: var(--black);
  color: var(--white);
}

.work-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 30px;
  min-height: 400px;
}

.grid-enter-active,
.grid-leave-active {
  transition: all 0.5s;
}

.grid-enter-from {
  opacity: 0;
  transform: translateY(30px);
}

.grid-leave-to {
  opacity: 0;
  transform: translateY(-30px);
}

.grid-move {
  transition: transform 0.5s;
}

.load-more {
  text-align: center;
  margin-top: 48px;
}

.load-more-btn {
  min-width: 200px;
  position: relative;
}

.loading-dots {
  display: inline-block;
  margin-left: 8px;
}

.loading-dots span {
  animation: blink 1.4s infinite both;
}

.loading-dots span:nth-child(2) {
  animation-delay: 0.2s;
}

.loading-dots span:nth-child(3) {
  animation-delay: 0.4s;
}

@keyframes blink {
  0%, 20%, 100% { opacity: 0; }
  50% { opacity: 1; }
}

@media (max-width: 768px) {
  .work-grid {
    grid-template-columns: 1fr;
  }
  
  .section-title {
    flex-direction: column;
    align-items: flex-start;
  }
  
  .title-decoration {
    width: 100%;
  }
}
</style>