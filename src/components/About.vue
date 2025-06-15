<script setup lang="ts">
import { onMounted, ref } from 'vue'
import { gsap } from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'

gsap.registerPlugin(ScrollTrigger)

const aboutRef = ref<HTMLElement>()
const imageRef = ref<HTMLElement>()
const contentRef = ref<HTMLElement>()

onMounted(() => {
  const tl = gsap.timeline({
    scrollTrigger: {
      trigger: aboutRef.value,
      start: 'top 80%',
      end: 'bottom 20%',
      toggleActions: 'play none none reverse'
    }
  });

  if (imageRef.value) {
    tl.fromTo(
      imageRef.value,
      { x: -100, opacity: 0, rotation: -10 },
      { x: 0, opacity: 1, rotation: 0, duration: 1.2, ease: 'power3.out' }
    );
  }

  if (contentRef.value) {
    tl.fromTo(
      contentRef.value,
      { x: 100, opacity: 0 },
      { x: 0, opacity: 1, duration: 1, ease: 'power3.out' },
      '-=0.8'
    );
  }
})
</script>

<template>
  <section id="about" ref="aboutRef" class="section about">
    <div class="container">
      <div class="about-grid">
        <div ref="imageRef" class="about-image">
          <div class="image-wrapper glass">
            <img 
              src="/public/img/WhatsApp Image 2025-06-07 at 11.49.19_124404c1.jpg" 
              alt="Muhammad Zikran Mazaya Rinadi"
              class="profile-image"
              style="filter: brightness(1.2) contrast(1.1);" 
            />
            <div class="glow-effect"></div>
          </div>
        </div>
        
        <div ref="contentRef" class="about-content">
          <h2 class="section-title">
            About <span class="gradient-text">Me</span>
          </h2>
          
          <p class="about-text">
            Hello! I'm Zikran, a passionate full-stack developer and designer with a love for 
            creating digital experiences that make a difference. I specialize in modern web 
            technologies and have a keen eye for user-centered design.
          </p>
          
          <p class="about-text">
            With expertise in React, Vue.js, Node.js, and modern design tools, I bridge the 
            gap between technical functionality and beautiful user interfaces. I believe that 
            great software should not only work perfectly but also feel intuitive and delightful to use.
          </p>
          
          <div class="stats">
            <div class="stat">
              <div class="stat-number gradient-text">10+</div>
              <div class="stat-label">Projects Completed</div>
            </div>
          </div>
          
          <a href="#contact" class="button">Let's Work Together</a>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.about {
  background: linear-gradient(135deg, rgba(0, 102, 255, 0.02) 0%, rgba(0, 255, 136, 0.02) 100%);
  padding: 6rem 0;
}

.about-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 4rem;
  align-items: center;
}

.about-image {
  position: relative;
}

.image-wrapper {
  position: relative;
  border-radius: 20px;
  overflow: hidden;
  transition: transform 0.3s ease;
}

.image-wrapper:hover {
  transform: translateY(-10px);
}

.profile-image {
  width: 100%;
  height: 500px;
  object-fit: cover;
  border-radius: 20px;
}

.glow-effect {
  position: absolute;
  top: -20px;
  left: -20px;
  right: -20px;
  bottom: -20px;
  background: linear-gradient(135deg, var(--primary), var(--secondary));
  border-radius: 30px;
  z-index: -1;
  opacity: 0.3;
  filter: blur(30px);
}

.section-title {
  font-size: clamp(2rem, 5vw, 3rem);
  font-weight: 700;
  margin-bottom: 2rem;
}

.about-text {
  font-size: 1.1rem;
  line-height: 1.8;
  color: var(--text-secondary);
  margin-bottom: 1.5rem;
}

.stats {
  display: flex;
  gap: 2rem;
  margin: 3rem 0;
}

.stat {
  text-align: center;
  flex: 1;
}

.stat-number {
  font-size: 2.5rem;
  font-weight: 700;
  line-height: 1;
  margin-bottom: 0.5rem;
}

.stat-label {
  font-size: 0.9rem;
  color: var(--text-secondary);
  text-transform: uppercase;
  letter-spacing: 1px;
}

/* Tablet Styles */
@media (max-width: 1024px) {
  .about {
    padding: 4rem 0;
  }
  
  .about-grid {
    gap: 3rem;
  }
  
  .profile-image {
    height: 400px;
  }
  
  .stats {
    gap: 1.5rem;
  }
  
  .stat-number {
    font-size: 2rem;
  }
}

/* Mobile Styles */
@media (max-width: 768px) {
  .about {
    padding: 3rem 0;
  }
  
  .about-grid {
    grid-template-columns: 1fr;
    gap: 2rem;
  }
  
  .stats {
    justify-content: space-around;
    gap: 1rem;
  }
  
  .profile-image {
    height: 300px;
  }
  
  .about-text {
    font-size: 1rem;
  }
}

/* Small Mobile Styles */
@media (max-width: 480px) {
  .about {
    padding: 2rem 0;
  }
  
  .stats {
    flex-direction: column;
    gap: 1.5rem;
  }
  
  .stat {
    padding: 1rem;
    background: rgba(255, 255, 255, 0.05);
    border-radius: 12px;
  }
  
  .profile-image {
    height: 250px;
  }
  
  .section-title {
    text-align: center;
  }
}
</style>