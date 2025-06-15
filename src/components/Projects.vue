<script setup lang="ts">
import { onMounted, ref } from 'vue'
import { gsap } from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'

gsap.registerPlugin(ScrollTrigger)

const projectsRef = ref<HTMLElement>()
const projects = ref([
  {
    title: 'Fatahillah Museum',
    description: 'A Fatahillah Museum website that makes it easy for visitors to see the collections and events at the museum',
    image: '/img/Screenshot 2025-05-25 142620.png',
    link: 'https://projek-museum.web.app/',
  },
  {
    title: 'Reservation Restaurant',
    description: 'A restaurant reservation website that makes it easy for people who want to make a reservation at the restaurant by filling in the existing form and being directed directly to WhatsApp.',
    image: '/img/Screenshot 2025-05-25 142636.png',
    link: 'https://projec1t-hometaste.web.app/',
  },
  {
    title: 'Website Tempat Makan',
    description: 'A website that is used to make it easier for buyers to order menus using only that website.',
    image: '/img/Screenshot 2025-05-25 222639.png',
    link: 'https://warungmakan-c7cc1.web.app/',
  },
  {
    title: 'TIX Flix',
    description: 'An application used to buy cinema tickets without having to queue.',
    image: '/img/Fatahillah Museum Website.jpg',
    link: 'https://www.figma.com/proto/4IEZ8fWvSY5VJ6Lhuj4kTe/TixFlix?node-id=107-981&p=f&t=519Lx89RhTbwmXKr-0&scaling=scale-down&content-scaling=fixed&page-id=0%3A1&starting-point-node-id=107%3A981',
  },
    {
    title: 'Management Employee',
    description: 'An android mobile application used to record employee leave.',
    image: '/img/Fatahillah Museum Website (1).jpg',
  },
    {
    title: 'Admin Adoption Exotic Animal',
    description: 'An admin website that functions to add every new animal and animal that has been adopted.',
    image: '/img/image2.png',
  }
])

onMounted(() => {
  const tl = gsap.timeline({
    scrollTrigger: {
      trigger: projectsRef.value,
      start: 'top 80%',
      toggleActions: 'play none none reverse'
    }
  })
  
  tl.fromTo('.project-card',
    { y: 100, opacity: 0, rotationY: 15 },
    { 
      y: 0, 
      opacity: 1, 
      rotationY: 0,
      duration: 0.8, 
      stagger: 0.2,
      ease: 'power3.out'
    }
  );
})
</script>

<template>
  <section id="projects" ref="projectsRef" class="section projects">
    <div class="container">
      <h2 class="section-title text-center">
        Featured <span class="gradient-text">Projects</span>
      </h2>
      
      <div class="projects-grid">
        <div 
          v-for="project in projects" 
          :key="project.title"
          class="project-card glass"
        >
          <div class="project-image">
            <img :src="project.image" :alt="project.title" />
            <div class="project-overlay">
              <div class="project-links">
                <a 
                  v-if="project.link" 
                  :href="project.link" 
                  class="project-link"
                  target="_blank" 
                  rel="noopener noreferrer"
                >
                  <span>View Live</span>
                  <svg width="16" height="16" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <path d="M18 13V19C18 19.5304 17.7893 20.0391 17.4142 20.4142C17.0391 20.7893 16.5304 21 16 21H5C4.46957 21 3.96086 20.7893 3.58579 20.4142C3.21071 20.0391 3 19.5304 3 19V8C3 7.46957 3.21071 6.96086 3.58579 6.58579C3.96086 6.21071 4.46957 6 5 6H11" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                    <path d="M15 3H21V9" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                    <path d="M10 14L21 3" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                  </svg>
                </a>
              </div>
            </div>
          </div>
          
          <div class="project-content">
            <h3 class="project-title">{{ project.title }}</h3>
            <p class="project-description">{{ project.description }}</p>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.projects {
  background: linear-gradient(135deg, rgba(255, 107, 107, 0.02) 0%, rgba(0, 102, 255, 0.02) 100%);
  padding: 6rem 0;
}

.section-title {
  font-size: clamp(2rem, 5vw, 3rem);
  font-weight: 700;
  margin-bottom: 4rem;
}

.text-center {
  text-align: center;
}

.projects-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
  gap: 2rem;
}

.project-card {
  overflow: hidden;
  transition: all 0.4s ease;
  cursor: pointer;
}

.project-card:hover {
  transform: translateY(-10px);
  box-shadow: 0 25px 50px rgba(0, 255, 136, 0.15);
}

.project-image {
  position: relative;
  overflow: hidden;
  height: 250px;
}

.project-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.4s ease;
}

.project-card:hover .project-image img {
  transform: scale(1.1);
}

.project-overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.8);
  display: flex;
  align-items: center;
  justify-content: center;
  opacity: 0;
  transition: opacity 0.3s ease;
}

.project-card:hover .project-overlay {
  opacity: 1;
}

.project-links {
  display: flex;
  gap: 1rem;
}

.project-link {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.8rem 1.5rem;
  background: var(--primary);
  color: var(--bg-dark);
  text-decoration: none;
  border-radius: 25px;
  font-weight: 600;
  transition: all 0.3s ease;
}

.project-link:hover {
  background: var(--secondary);
  transform: translateY(-2px);
}

.project-content {
  padding: 2rem;
}

.project-title {
  font-size: 1.4rem;
  font-weight: 700;
  margin-bottom: 1rem;
  color: var(--text-primary);
}

.project-description {
  color: var(--text-secondary);
  line-height: 1.6;
  margin-bottom: 1.5rem;
}

.project-technologies {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
}

.tech-tag {
  background: rgba(0, 255, 136, 0.1);
  color: var(--primary);
  padding: 0.3rem 0.8rem;
  border-radius: 15px;
  font-size: 0.85rem;
  font-weight: 500;
  border: 1px solid rgba(0, 255, 136, 0.2);
}

/* Tablet Styles */
@media (max-width: 1024px) {
  .projects {
    padding: 4rem 0;
  }
  
  .projects-grid {
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 1.5rem;
  }
  
  .project-content {
    padding: 1.5rem;
  }
}

/* Mobile Styles */
@media (max-width: 768px) {
  .projects {
    padding: 3rem 0;
  }
  
  .projects-grid {
    grid-template-columns: 1fr;
    gap: 1.5rem;
  }
  
  .project-links {
    flex-direction: column;
    gap: 0.8rem;
  }
  
  .project-link {
    justify-content: center;
  }
  
  .project-image {
    height: 200px;
  }
}

/* Small Mobile Styles */
@media (max-width: 480px) {
  .projects {
    padding: 2rem 0;
  }
  
  .project-content {
    padding: 1rem;
  }
  
  .project-title {
    font-size: 1.2rem;
  }
  
  .project-description {
    font-size: 0.9rem;
  }
  
  .tech-tag {
    font-size: 0.8rem;
    padding: 0.2rem 0.6rem;
  }
}
</style>