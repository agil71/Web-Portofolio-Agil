<template>
  <transition name="modal">
    <div v-if="isOpen" class="modal-overlay" @click.self="closeModal">
      <div class="modal-container">
        <button class="modal-close" @click="closeModal">&times;</button>
        
        <div class="modal-header">
          <span class="modal-icon">📬</span>
          <h2>Get In Touch</h2>
          <p>Feel free to reach out through any of these channels</p>
        </div>
        
        <div class="modal-content">
          <!-- Email -->
          <a href="mailto:ajimunawar24@gmail.com" class="contact-item email">
            <span class="contact-icon">📧</span>
            <div class="contact-info">
              <span class="contact-label">Email</span>
              <span class="contact-value">ajimunawar24@gmail.com</span>
            </div>
            <span class="contact-action">Send Email →</span>
          </a>
          
          <!-- WhatsApp -->
          <a href="https://wa.me/6282131258360" target="_blank" class="contact-item whatsapp">
            <span class="contact-icon">💬</span>
            <div class="contact-info">
              <span class="contact-label">WhatsApp</span>
              <span class="contact-value">+62 821 3125 8360</span>
            </div>
            <span class="contact-action">Chat Now →</span>
          </a>
          
          <!-- Instagram -->
          <a href="https://instagram.com/ajiik.m" target="_blank" class="contact-item instagram">
            <span class="contact-icon">📷</span>
            <div class="contact-info">
              <span class="contact-label">Instagram</span>
              <span class="contact-value">@ajiik.m</span>
            </div>
            <span class="contact-action">Follow →</span>
          </a>
          
          <!-- GitHub -->
          <a href="https://github.com/agil71" target="_blank" class="contact-item github">
            <span class="contact-icon">🐙</span>
            <div class="contact-info">
              <span class="contact-label">GitHub</span>
              <span class="contact-value">agil71</span>
            </div>
            <span class="contact-action">View Profile →</span>
          </a>
          
          <!-- Facebook -->
          <a href="https://www.facebook.com/ajik.m.167" target="_blank" class="contact-item facebook">
            <span class="contact-icon">👤</span>
            <div class="contact-info">
              <span class="contact-label">Facebook</span>
              <span class="contact-value">Ajik M</span>
            </div>
            <span class="contact-action">Connect →</span>
          </a>
        </div>
        
        <div class="modal-footer">
          <button class="copy-email-btn" @click="copyEmail">
            <span v-if="!copied">📋 Copy Email</span>
            <span v-else>✅ Copied!</span>
          </button>
          <p class="modal-note">Response time: within 24 hours</p>
        </div>
      </div>
    </div>
  </transition>
</template>

<script setup>
import { ref } from 'vue'

const props = defineProps({
  isOpen: {
    type: Boolean,
    default: false
  }
})

const emit = defineEmits(['close'])
const copied = ref(false)

const closeModal = () => {
  emit('close')
}

const copyEmail = async () => {
  try {
    await navigator.clipboard.writeText('ajimunawar24@gmail.com')
    copied.value = true
    setTimeout(() => {
      copied.value = false
    }, 2000)
  } catch (err) {
    alert('Failed to copy email')
  }
}
</script>

<style scoped>
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.8);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 2000;
  backdrop-filter: blur(5px);
  padding: 20px;
}

.modal-container {
  background: var(--white);
  border: 4px solid var(--black);
  box-shadow: 16px 16px 0 var(--black);
  max-width: 500px;
  width: 100%;
  max-height: 90vh;
  overflow-y: auto;
  position: relative;
  animation: modalPop 0.3s;
}

@keyframes modalPop {
  0% {
    transform: scale(0.8);
    opacity: 0;
  }
  100% {
    transform: scale(1);
    opacity: 1;
  }
}

.modal-close {
  position: absolute;
  top: 16px;
  right: 16px;
  background: var(--white);
  border: 2px solid var(--black);
  width: 40px;
  height: 40px;
  font-size: 1.8rem;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: all 0.2s;
  z-index: 10;
}

.modal-close:hover {
  background: var(--magenta);
  color: white;
  transform: rotate(90deg);
}

.modal-header {
  text-align: center;
  padding: 40px 32px 24px;
  border-bottom: 2px dashed var(--black);
}

.modal-icon {
  font-size: 3.5rem;
  display: block;
  margin-bottom: 16px;
  animation: bounce 1s infinite;
}

@keyframes bounce {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(-5px); }
}

.modal-header h2 {
  font-size: 2rem;
  font-weight: 700;
  margin-bottom: 8px;
  text-transform: uppercase;
}

.modal-header p {
  color: #666;
  font-size: 0.95rem;
}

.modal-content {
  padding: 24px;
  display: flex;
  flex-direction: column;
  gap: 12px;
}

.contact-item {
  display: flex;
  align-items: center;
  gap: 16px;
  padding: 16px;
  text-decoration: none;
  color: var(--black);
  border: 2px solid var(--black);
  transition: all 0.2s;
  background: var(--white);
}

.contact-item:hover {
  transform: translate(-4px, -4px);
  box-shadow: 8px 8px 0 var(--black);
}

.contact-item.email:hover {
  background: #ea4335;
  color: white;
  border-color: #ea4335;
}

.contact-item.whatsapp:hover {
  background: #25d366;
  color: white;
  border-color: #25d366;
}

.contact-item.instagram:hover {
  background: #e4405f;
  color: white;
  border-color: #e4405f;
}

.contact-item.github:hover {
  background: #333;
  color: white;
  border-color: #333;
}

.contact-item.facebook:hover {
  background: #1877f2;
  color: white;
  border-color: #1877f2;
}

.contact-icon {
  font-size: 1.8rem;
  min-width: 40px;
  text-align: center;
}

.contact-info {
  flex: 1;
  display: flex;
  flex-direction: column;
  gap: 4px;
}

.contact-label {
  font-size: 0.75rem;
  text-transform: uppercase;
  font-weight: 600;
  opacity: 0.7;
}

.contact-value {
  font-weight: 700;
  font-size: 1rem;
}

.contact-action {
  font-size: 0.85rem;
  font-weight: 600;
  opacity: 0;
  transition: opacity 0.2s;
}

.contact-item:hover .contact-action {
  opacity: 1;
}

.modal-footer {
  padding: 24px;
  text-align: center;
  border-top: 2px dashed var(--black);
}

.copy-email-btn {
  padding: 12px 24px;
  background: var(--yellow);
  border: 2px solid var(--black);
  font-weight: 700;
  font-size: 1rem;
  cursor: pointer;
  transition: all 0.2s;
  margin-bottom: 12px;
}

.copy-email-btn:hover {
  transform: translate(-2px, -2px);
  box-shadow: 4px 4px 0 var(--black);
}

.modal-note {
  font-size: 0.8rem;
  color: #666;
}

/* Modal Transition */
.modal-enter-active,
.modal-leave-active {
  transition: opacity 0.3s;
}

.modal-enter-from,
.modal-leave-to {
  opacity: 0;
}

.modal-enter-from .modal-container,
.modal-leave-to .modal-container {
  transform: scale(0.8);
}

@media (max-width: 600px) {
  .modal-container {
    max-width: 100%;
  }
  
  .modal-header {
    padding: 32px 20px 20px;
  }
  
  .modal-content {
    padding: 16px;
  }
  
  .contact-item {
    padding: 12px;
  }
  
  .contact-value {
    font-size: 0.9rem;
  }
  
  .contact-action {
    display: none;
  }
}
</style>