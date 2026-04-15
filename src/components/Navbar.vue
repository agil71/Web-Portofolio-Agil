<template>
  <nav class="navbar" :class="{ 'navbar-scrolled': isScrolled }">
    <div class="container nav-container">
      <div class="logo" @click="scrollToTop">
        <a href="#">PORTOFOLIO<span class="dot">.</span></a>
      </div>
      <div class="nav-links">
        <a 
          v-for="link in navLinks" 
          :key="link.id"
          @click.prevent="scrollToSection(link.id)"
          :class="{ 'active': activeSection === link.id }"
          href="#"
        >
          {{ link.text }}
          <span class="link-underline"></span>
        </a>
      </div>
      <!-- HIRE ME BUTTON - OPEN MODAL -->
      <button class="nb-button nav-cta" @click="handleHireMe">
        <span class="btn-text">Hire Me</span>
        <span class="btn-icon">→</span>
        <div class="btn-glitch"></div>
      </button>
    </div>
  </nav>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const emit = defineEmits(['open-contact'])

const isScrolled = ref(false)
const activeSection = ref('work')

const navLinks = [
  { id: 'work', text: 'Work' },
  { id: 'download-cv', text: 'CV' },
  { id: 'about', text: 'About' }
]

const handleScroll = () => {
  isScrolled.value = window.scrollY > 50
  
  const sections = navLinks.map(link => link.id)
  for (const section of sections) {
    const element = document.getElementById(section)
    if (element) {
      const rect = element.getBoundingClientRect()
      if (rect.top <= 150 && rect.bottom >= 150) {
        activeSection.value = section
        break
      }
    }
  }
}

const scrollToSection = (id) => {
  const element = document.getElementById(id)
  if (element) {
    element.scrollIntoView({ behavior: 'smooth' })
    activeSection.value = id
  }
}

const scrollToTop = () => {
  window.scrollTo({ top: 0, behavior: 'smooth' })
}

const handleHireMe = () => {
  emit('open-contact')
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll)
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})
</script>

<style scoped>
.navbar {
  padding: 24px 0;
  background: var(--white);
  border-bottom: var(--border);
  position: sticky;
  top: 0;
  z-index: 1000;
  transition: all 0.3s ease;
}

.navbar-scrolled {
  padding: 16px 0;
  box-shadow: 0 4px 0 var(--black);
}

.nav-container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  position: relative;
}

.logo {
  cursor: pointer;
  transition: transform 0.2s;
}

.logo:hover {
  transform: scale(1.05) rotate(-2deg);
}

.logo a {
  font-size: 2rem;
  font-weight: 700;
  text-decoration: none;
  color: var(--black);
  letter-spacing: -0.02em;
  transition: color 0.2s;
}

.logo .dot {
  color: var(--magenta);
  display: inline-block;
  animation: pulse 2s infinite;
}

@keyframes pulse {
  0%, 100% { transform: scale(1); }
  50% { transform: scale(1.1); }
}

.nav-links {
  display: flex;
  list-style: none;
  gap: 48px;
}

.nav-links a {
  text-decoration: none;
  color: var(--black);
  font-weight: 600;
  font-size: 1.1rem;
  text-transform: uppercase;
  padding: 8px 0;
  position: relative;
  transition: all 0.3s;
}

.link-underline {
  position: absolute;
  bottom: 0;
  left: 0;
  width: 0;
  height: 3px;
  background: var(--magenta);
  transition: width 0.3s ease;
}

.nav-links a:hover .link-underline,
.nav-links a.active .link-underline {
  width: 100%;
}

.nav-links a.active {
  color: var(--magenta);
}

.nav-cta {
  font-size: 0.9rem;
  padding: 8px 20px;
  position: relative;
  overflow: hidden;
}

.btn-text {
  position: relative;
  z-index: 2;
  transition: transform 0.3s;
}

.btn-icon {
  position: relative;
  z-index: 2;
  margin-left: 8px;
  transition: transform 0.3s;
  display: inline-block;
}

.nav-cta:hover .btn-text {
  transform: translateX(-4px);
}

.nav-cta:hover .btn-icon {
  transform: translateX(4px);
}

.btn-glitch {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: var(--magenta);
  transform: translateX(-100%);
  transition: transform 0.3s;
  z-index: 1;
}

.nav-cta:hover .btn-glitch {
  transform: translateX(0);
}

.nav-cta:hover {
  color: var(--white);
}

.ripple {
  position: absolute;
  border-radius: 50%;
  background: rgba(255, 255, 255, 0.5);
  transform: scale(0);
  animation: ripple-animation 0.6s ease-out;
  pointer-events: none;
  z-index: 3;
}

@keyframes ripple-animation {
  to {
    transform: scale(4);
    opacity: 0;
  }
}

/* Mobile Menu */
.mobile-menu-toggle {
  display: none;
  flex-direction: column;
  gap: 6px;
  background: none;
  border: none;
  cursor: pointer;
  padding: 8px;
}

.mobile-menu-toggle span {
  width: 30px;
  height: 3px;
  background: var(--black);
  transition: all 0.3s;
}

.mobile-menu {
  display: none;
  position: absolute;
  top: 100%;
  left: 0;
  right: 0;
  background: var(--white);
  border-bottom: var(--border);
  padding: 20px;
  flex-direction: column;
  gap: 16px;
  transform: translateY(-100%);
  transition: transform 0.3s;
  z-index: -1;
}

.mobile-menu.active {
  transform: translateY(0);
}

.mobile-menu a {
  text-decoration: none;
  color: var(--black);
  font-weight: 600;
  font-size: 1.2rem;
  text-transform: uppercase;
  padding: 12px;
  border: 2px solid var(--black);
  text-align: center;
  transition: all 0.2s;
}

.mobile-menu a:hover {
  background: var(--yellow);
  transform: translate(-2px, -2px);
  box-shadow: 4px 4px 0 var(--black);
}

@media (max-width: 768px) {
  .nav-links {
    display: none;
  }
  
  .mobile-menu-toggle {
    display: flex;
  }
  
  .mobile-menu {
    display: flex;
  }
}
</style>