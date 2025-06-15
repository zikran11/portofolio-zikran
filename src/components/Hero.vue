<script setup lang="ts">
import { onMounted, ref } from 'vue'
import { gsap } from 'gsap'

const heroRef = ref<HTMLElement>()
const titleRef = ref<HTMLElement>()
const subtitleRef = ref<HTMLElement>()
const descriptionRef = ref<HTMLElement>()
const ctaRef = ref<HTMLElement>()

onMounted(() => {
  const tl = gsap.timeline();

  if (titleRef.value) {
    tl.fromTo(
      titleRef.value,
      { y: 100, opacity: 0 },
      { y: 0, opacity: 1, duration: 1.2, ease: 'power3.out' }
    );
  }

  if (subtitleRef.value) {
    tl.fromTo(
      subtitleRef.value,
      { y: 50, opacity: 0 },
      { y: 0, opacity: 1, duration: 1, ease: 'power3.out' },
      '-=0.5'
    );
  }

  if (descriptionRef.value) {
    tl.fromTo(
      descriptionRef.value,
      { y: 30, opacity: 0 },
      { y: 0, opacity: 1, duration: 0.8, ease: 'power3.out' },
      '-=0.3'
    );
  }

  if (ctaRef.value) {
    tl.fromTo(
      ctaRef.value,
      { y: 20, opacity: 0 },
      { y: 0, opacity: 1, duration: 0.6, ease: 'power3.out' },
      '-=0.2'
    );
  }

  if (heroRef.value) {
    // Floating animation for the hero content
    gsap.to(heroRef.value, {
      y: -20,
      duration: 3,
      repeat: -1,
      yoyo: true,
      ease: 'power2.inOut',
    });
  }
});

const scrollToProjects = () => {
  const element = document.getElementById('projects')
  if (element) {
    element.scrollIntoView({ behavior: 'smooth' })
  }
}
</script>

<template>
  <section id="hero" class="section hero">
    <div class="container">
      <div ref="heroRef" class="hero-content">
        <h1 ref="titleRef" class="hero-title">
          <span class="gradient-text">Muhammad Zikran</span><br>
          <span class="neon-glow">Mazaya Rinadi</span>
        </h1>
        
        <h2 ref="subtitleRef" class="hero-subtitle">
          Web Developer & UI/UX Designer
        </h2>
        
        <div ref="ctaRef" class="hero-cta">
          <button @click="scrollToProjects" class="button">
            View My Work
          </button>
            <a href="/CV MUHAMMAD ZIKRAN MAZAYA RINADI (ENG).pdf" class="button-outline" download>
            Download CV
          </a>
        </div>
      </div>
      
      <div class="hero-visual">
        <div class="floating-elements">
          <div class="element element-1"></div>
          <div class="element element-2"></div>
          <div class="element element-3"></div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.hero {
  position: relative;
  background: radial-gradient(ellipse at center, rgba(0, 255, 136, 0.05) 0%, transparent 70%);
  padding-top: 120px; /* Add padding to account for fixed navbar */
}

.hero-content {
  max-width: 600px;
  z-index: 2;
  position: relative;
}

.hero-title {
  font-size: clamp(2.5rem, 8vw, 4.5rem);
  font-weight: 700;
  line-height: 1.1;
  margin-bottom: 1rem;
}

.hero-subtitle {
  font-size: clamp(1.2rem, 3vw, 1.8rem);
  color: var(--text-secondary);
  font-weight: 500;
  margin-bottom: 2rem;
  font-family: 'JetBrains Mono', monospace;
}

.hero-description {
  font-size: 1.2rem;
  color: var(--text-secondary);
  line-height: 1.8;
  margin-bottom: 3rem;
  max-width: 500px;
}

.hero-cta {
  display: flex;
  gap: 1.5rem;
  flex-wrap: wrap;
}

.button-outline {
  padding: 1rem 2rem;
  border: 2px solid var(--primary);
  border-radius: 50px;
  color: var(--primary);
  text-decoration: none;
  font-weight: 600;
  transition: all 0.3s ease;
  background: transparent;
}

.button-outline:hover {
  background: var(--primary);
  color: var(--bg-dark);
  transform: translateY(-2px);
  box-shadow: 0 10px 30px rgba(0, 255, 136, 0.3);
}

.hero-visual {
  position: absolute;
  top: 0;
  right: 0;
  width: 50%;
  height: 100%;
  z-index: 1;
}

.floating-elements {
  position: relative;
  width: 100%;
  height: 100%;
}

.element {
  position: absolute;
  border-radius: 50%;
  opacity: 0.1;
  animation: float 6s ease-in-out infinite;
}

.element-1 {
  width: 200px;
  height: 200px;
  background: var(--primary);
  top: 20%;
  right: 20%;
  animation-delay: 0s;
}

.element-2 {
  width: 100px;
  height: 100px;
  background: var(--secondary);
  top: 60%;
  right: 40%;
  animation-delay: 2s;
}

.element-3 {
  width: 150px;
  height: 150px;
  background: var(--accent);
  top: 40%;
  right: 60%;
  animation-delay: 4s;
}

@keyframes float {
  0%, 100% { transform: translateY(0px) rotate(0deg); }
  50% { transform: translateY(-20px) rotate(180deg); }
}

@media (max-width: 768px) {
  .hero {
    padding-top: 100px; /* Slightly less padding on mobile */
  }
  
  .hero-visual {
    display: none;
  }
  
  .hero-cta {
    flex-direction: column;
    align-items: flex-start;
  }
  
  .button, .button-outline {
    width: 100%;
    text-align: center;
  }
}

@media (max-width: 480px) {
  .hero {
    padding-top: 90px; /* Even less padding on very small screens */
  }
}
</style>