<template>
  <section id="download-cv" class="download-section">
    <div class="container">
      <div class="download-wrapper">
        <div class="download-info">
          <h2 class="section-title">Download My CV</h2>
          <p class="download-description">
            Get my complete resume to learn more about my experience and skills.
          </p>
        </div>
        <div class="download-action">
          <a 
            href="CV_AgilAjiMunawar.pdf" 
            download 
            class="nb-button cv-button"
          >
            <span>Download CV</span>
            <span class="arrow">↓</span>
          </a>
          <p class="cv-note">PDF • 3 KB</p>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.download-section {
  padding: 80px 0;
  background: var(--white);
  border-top: var(--border);
  border-bottom: var(--border);
}

.download-wrapper {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 40px;
}

.download-info {
  flex: 1;
}

.section-title {
  font-size: 2.5rem;
  font-weight: 700;
  margin-bottom: 16px;
  text-transform: uppercase;
  border-left: 8px solid var(--magenta);
  padding-left: 24px;
}

.download-description {
  font-size: 1.2rem;
  color: #444;
}

.download-action {
  text-align: center;
}

.cv-button {
  font-size: 1.2rem;
  padding: 16px 32px;
  display: inline-flex;
  align-items: center;
  gap: 12px;
}

.cv-button:hover {
  transform: translate(4px, 4px);
  box-shadow: 4px 4px 0 var(--black);
}

.arrow {
  font-size: 1.5rem;
}

.cv-note {
  margin-top: 12px;
  font-size: 0.9rem;
  color: #666;
}

@media (max-width: 768px) {
  .download-wrapper {
    flex-direction: column;
    text-align: center;
  }
  
  .section-title {
    border-left: none;
    border-bottom: 4px solid var(--magenta);
    padding-left: 0;
    padding-bottom: 16px;
    display: inline-block;
  }
}
</style>
