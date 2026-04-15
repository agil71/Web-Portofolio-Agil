<template>
  <section id="about" class="about">
    <div class="container">
      <div class="about-wrapper nb-card">
        <div class="about-info">
          <h2 class="section-title">About Me</h2>
          <div class="about-content">
            <p class="about-intro">
              Hi! I'm <strong>Agil Aji Munawar</strong>, a passionate Front-end Developer 
              and UI enthusiast based in Samarinda, Indonesia.
            </p>
            <p class="about-text">
              I'm currently studying Computer Science at Mulawarman University. 
              I love crafting bold, accessible web applications with brutalist 
              design principles that make a statement.
            </p>
            <p class="about-text">
              Every interface I build is intentional, honest, and structurally bold. 
              I believe design should be raw, functional, and unapologetically unique.
            </p>
            
            <div class="about-details">
              <div class="detail-item">
                <span class="detail-label">📍 Location</span>
                <span class="detail-value">Samarinda, Indonesia</span>
              </div>
              <div class="detail-item">
                <span class="detail-label">🎓 Education</span>
                <span class="detail-value">Computer Science - UNMUL</span>
              </div>
              <!-- <div class="detail-item">
                <span class="detail-label">💼 Experience</span>
                <span class="detail-value">5+ Years</span>
              </div> -->
              <div class="detail-item">
                <span class="detail-label">📧 Email</span>
                <a href="mailto:ajimunawar24@gmail.com" class="email-link">
                  ajimunawar24@gmail.com
                </a>
              </div>
            </div>
          </div>
        </div>
        
        <div class="about-quote">
          <div class="quote-icon">"</div>
          <p class="quote-text">
            Design with intention, code with brutality.
          </p>
          <div class="quote-author">— Agil Aji</div>
          
          <div class="social-links">
            <a href="https://github.com/agil71" target="_blank" class="social-link">
              <span>GitHub</span>
              <span class="arrow">↗</span>
            </a>
            <a href="https://instagram.com/ajiik.m" target="_blank" class="social-link">
              <span>Instagram</span>
              <span class="arrow">↗</span>
            </a>
            <a href="https://wa.me/6282131258360" target="_blank" class="social-link">
              <span>WhatsApp</span>
              <span class="arrow">↗</span>
            </a>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.about {
  padding: 80px 0;
  background: var(--bg);
}

.about-wrapper {
  display: grid;
  grid-template-columns: 1.5fr 1fr;
  gap: 48px;
  padding: 48px;
}

.section-title {
  font-size: 2.5rem;
  font-weight: 700;
  margin-bottom: 32px;
  text-transform: uppercase;
  border-left: 8px solid var(--magenta);
  padding-left: 24px;
}

.about-intro {
  font-size: 1.5rem;
  font-weight: 500;
  margin-bottom: 24px;
  line-height: 1.4;
}

.about-intro strong {
  background: var(--yellow);
  padding: 0 4px;
  border: 2px solid var(--black);
}

.about-text {
  font-size: 1.1rem;
  margin-bottom: 16px;
  color: #444;
  line-height: 1.6;
}

.about-details {
  margin-top: 32px;
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 20px;
}

.detail-item {
  display: flex;
  flex-direction: column;
  gap: 4px;
}

.detail-label {
  font-size: 0.8rem;
  text-transform: uppercase;
  font-weight: 600;
  color: #666;
  letter-spacing: 0.05em;
}

.detail-value {
  font-size: 1.1rem;
  font-weight: 600;
}

.email-link {
  color: var(--black);
  text-decoration: none;
  border-bottom: 2px solid var(--magenta);
  padding-bottom: 2px;
  transition: all 0.2s;
}

.email-link:hover {
  color: var(--magenta);
  border-bottom-width: 4px;
}

.about-quote {
  background: var(--white);
  border: 3px solid var(--black);
  padding: 32px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  position: relative;
}

.quote-icon {
  font-size: 5rem;
  font-family: serif;
  line-height: 1;
  color: var(--magenta);
  margin-bottom: 16px;
}

.quote-text {
  font-size: 1.8rem;
  font-weight: 700;
  line-height: 1.3;
  margin-bottom: 16px;
  text-transform: uppercase;
}

.quote-author {
  font-size: 1rem;
  color: #666;
  margin-bottom: 32px;
}

.social-links {
  display: flex;
  flex-direction: column;
  gap: 12px;
}

.social-link {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 12px 0;
  text-decoration: none;
  color: var(--black);
  font-weight: 600;
  font-size: 1.1rem;
  border-bottom: 2px solid var(--black);
  transition: all 0.2s;
}

.social-link:hover {
  padding-left: 8px;
  color: var(--magenta);
  border-bottom-color: var(--magenta);
}

.social-link .arrow {
  transition: transform 0.2s;
}

.social-link:hover .arrow {
  transform: translate(4px, -4px);
}

@media (max-width: 768px) {
  .about-wrapper {
    grid-template-columns: 1fr;
    padding: 24px;
  }
  
  .about-details {
    grid-template-columns: 1fr;
  }
  
  .section-title {
    font-size: 2rem;
  }
  
  .about-intro {
    font-size: 1.3rem;
  }
  
  .quote-text {
    font-size: 1.5rem;
  }
}
</style>