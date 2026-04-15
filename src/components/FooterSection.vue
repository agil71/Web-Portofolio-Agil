<template>
  <footer class="footer">
    <div class="container">
      <div class="footer-content">
        <div class="footer-logo">
          <span>PORTOFOLIO<span class="dot">.</span></span>
        </div>
        <div class="footer-copyright">
          © {{ currentYear }} — Neo Brutalist Portfolio
        </div>
        <div class="footer-links">
          <a href="#">Privacy</a>
          <span class="separator">|</span>
          <a href="#">Imprint</a>
        </div>
      </div>
    </div>
  </footer>
</template>

<script setup>
const currentYear = new Date().getFullYear()
</script>

<style scoped>
.footer {
  padding: 32px 0;
  background: var(--black);
  color: var(--white);
  border-top: 4px solid var(--yellow);
  margin-top: auto;
}

.footer-content {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.footer-logo {
  font-size: 1.5rem;
  font-weight: 700;
}

.footer-logo .dot {
  color: var(--yellow);
}

.footer-copyright {
  font-size: 0.9rem;
  opacity: 0.8;
}

.footer-links {
  display: flex;
  gap: 12px;
}

.footer-links a {
  color: var(--white);
  text-decoration: none;
  font-weight: 500;
}

.footer-links a:hover {
  color: var(--yellow);
}

.separator {
  opacity: 0.5;
}

@media (max-width: 640px) {
  .footer-content {
    flex-direction: column;
    gap: 16px;
    text-align: center;
  }
}
</style>