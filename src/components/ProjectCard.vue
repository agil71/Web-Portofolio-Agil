<template>
  <article 
    class="nb-card project-card" 
    @click="toggleExpand"
    :class="{ 'expanded': isExpanded }"
    @mousemove="handleMouseMove"
    @mouseleave="handleMouseLeave"
  >
    <div class="card-glow" :style="glowStyle"></div>
    
    <div class="project-image" :style="{ background: project.color || '#00e5ff' }">
      <!-- GAMBAR PROJECT -->
      <img 
        v-if="project.image && !imageError"
        :src="project.image" 
        :alt="project.title"
        class="project-thumbnail"
        @error="handleImageError"
      />
      <!-- FALLBACK EMOJI -->
      <span v-else class="project-emoji">{{ project.emoji || '📁' }}</span>
      
      <div class="image-overlay">
        <span class="view-text">View Details</span>
      </div>
    </div>
    
    <div class="project-content">
      <span class="project-category">{{ project.category }}</span>
      <h3 class="project-title">{{ project.title }}</h3>
      <p class="project-description">{{ project.description }}</p>
      
      <div class="project-tags">
        <span 
          v-for="tag in project.tags" 
          :key="tag" 
          class="tag"
          @click.stop="filterByTag(tag)"
        >
          {{ tag }}
        </span>
      </div>
      
      <!-- Expanded Content -->
      <transition name="expand">
        <div v-if="isExpanded" class="project-expanded">
          <p class="project-detail">{{ project.detail }}</p>
          <div class="project-meta">
            <div class="meta-item">
              <span class="meta-label">Timeline</span>
              <span class="meta-value">{{ project.timeline }}</span>
            </div>
            <div class="meta-item">
              <span class="meta-label">Role</span>
              <span class="meta-value">{{ project.role }}</span>
            </div>
          </div>
        </div>
      </transition>
      
      <div class="project-footer">
        <a href="#" class="project-link" @click.prevent.stop="handleViewProject">
          {{ isExpanded ? 'Show Less' : 'View Project' }}
          <span class="arrow">{{ isExpanded ? '↑' : '↗' }}</span>
        </a>
        <button class="like-btn" @click.stop="toggleLike" :class="{ 'liked': isLiked }">
          <span class="like-icon">{{ isLiked ? '❤️' : '🤍' }}</span>
          <span class="like-count">{{ likeCount }}</span>
        </button>
      </div>
    </div>
  </article>
</template>

<script setup>
import { ref, computed } from 'vue'

const props = defineProps({
  project: {
    type: Object,
    required: true
  }
})

const emit = defineEmits(['filter-tag', 'view-project'])

const isExpanded = ref(false)
const isLiked = ref(false)
const likeCount = ref(Math.floor(Math.random() * 50) + 10)
const mouseX = ref(0)
const mouseY = ref(0)
const imageError = ref(false)

const glowStyle = computed(() => ({
  background: `radial-gradient(circle at ${mouseX.value}px ${mouseY.value}px, rgba(255,255,255,0.1) 0%, transparent 50%)`
}))

const handleImageError = () => {
  imageError.value = true
}

const toggleExpand = () => {
  isExpanded.value = !isExpanded.value
}

const toggleLike = () => {
  isLiked.value = !isLiked.value
  likeCount.value += isLiked.value ? 1 : -1
}

const filterByTag = (tag) => {
  emit('filter-tag', tag)
}

const handleViewProject = () => {
  emit('view-project', props.project)
}

const handleMouseMove = (e) => {
  const rect = e.currentTarget.getBoundingClientRect()
  mouseX.value = e.clientX - rect.left
  mouseY.value = e.clientY - rect.top
}

const handleMouseLeave = () => {
  mouseX.value = 0
  mouseY.value = 0
}
</script>

<style scoped>
.project-card {
  padding: 0;
  overflow: hidden;
  display: flex;
  flex-direction: column;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  position: relative;
  cursor: pointer;
}

.card-glow {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
  z-index: 1;
  opacity: 0;
  transition: opacity 0.3s;
}

.project-card:hover .card-glow {
  opacity: 1;
}

.project-card:hover {
  transform: translate(-4px, -4px);
  box-shadow: 12px 12px 0 var(--black);
}

.project-image {
  height: 220px;
  display: flex;
  align-items: center;
  justify-content: center;
  border-bottom: var(--border);
  position: relative;
  overflow: hidden;
}

.project-thumbnail {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.4s;
}

.project-card:hover .project-thumbnail {
  transform: scale(1.1);
}

.project-emoji {
  font-size: 5rem;
  transition: transform 0.3s;
}

.project-card:hover .project-emoji {
  transform: scale(1.1) rotate(5deg);
}

.image-overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.7);
  display: flex;
  align-items: center;
  justify-content: center;
  opacity: 0;
  transition: opacity 0.3s;
}

.project-card:hover .image-overlay {
  opacity: 1;
}

.view-text {
  color: white;
  font-weight: 700;
  text-transform: uppercase;
  padding: 12px 24px;
  border: 3px solid white;
  background: rgba(0, 0, 0, 0.5);
}

.project-content {
  padding: 24px;
  position: relative;
  z-index: 2;
  background: var(--white);
}

.project-category {
  font-size: 0.8rem;
  text-transform: uppercase;
  font-weight: 600;
  color: #666;
  letter-spacing: 0.05em;
}

.project-title {
  font-size: 1.75rem;
  font-weight: 700;
  margin: 8px 0 12px;
  line-height: 1.2;
  transition: color 0.3s;
}

.project-card:hover .project-title {
  color: var(--magenta);
}

.project-description {
  margin-bottom: 16px;
  color: #444;
}

.project-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
  margin-bottom: 20px;
}

.tag {
  padding: 4px 12px;
  background: var(--bg);
  border: 2px solid var(--black);
  font-size: 0.8rem;
  font-weight: 600;
  transition: all 0.2s;
  cursor: pointer;
  position: relative;
  z-index: 3;
}

.tag:hover {
  background: var(--yellow);
  transform: translate(-1px, -1px);
  box-shadow: 2px 2px 0 var(--black);
}

.project-expanded {
  margin-top: 20px;
  padding-top: 20px;
  border-top: 2px dashed var(--black);
}

.expand-enter-active,
.expand-leave-active {
  transition: all 0.3s;
}

.expand-enter-from,
.expand-leave-to {
  opacity: 0;
  transform: translateY(-10px);
}

.project-detail {
  margin-bottom: 16px;
  color: #555;
  line-height: 1.6;
}

.project-meta {
  display: flex;
  gap: 24px;
}

.meta-item {
  display: flex;
  flex-direction: column;
}

.meta-label {
  font-size: 0.7rem;
  text-transform: uppercase;
  color: #666;
  font-weight: 600;
}

.meta-value {
  font-weight: 700;
  font-size: 1.1rem;
}

.project-footer {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.project-link {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  text-decoration: none;
  color: var(--black);
  font-weight: 700;
  text-transform: uppercase;
  border-bottom: 3px solid var(--black);
  padding-bottom: 4px;
  transition: all 0.3s;
  position: relative;
  z-index: 3;
}

.project-link:hover {
  color: var(--magenta);
  border-bottom-color: var(--magenta);
}

.arrow {
  font-size: 1.2rem;
  transition: transform 0.3s;
  display: inline-block;
}

.project-link:hover .arrow {
  transform: translate(4px, -4px);
}

.like-btn {
  background: none;
  border: 2px solid var(--black);
  padding: 8px 16px;
  cursor: pointer;
  display: flex;
  align-items: center;
  gap: 8px;
  font-weight: 600;
  transition: all 0.2s;
  position: relative;
  z-index: 3;
}

.like-btn:hover {
  background: var(--yellow);
  transform: scale(1.05);
}

.like-btn.liked {
  background: #ffebee;
  border-color: #ff5252;
}

.like-icon {
  font-size: 1.2rem;
  transition: transform 0.3s;
}

.like-btn:hover .like-icon {
  transform: scale(1.2);
}

.like-btn.liked .like-icon {
  animation: heartBeat 0.3s;
}

@keyframes heartBeat {
  0%, 100% { transform: scale(1); }
  50% { transform: scale(1.3); }
}
</style>