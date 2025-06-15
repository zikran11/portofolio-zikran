<script setup lang="ts">
import { onMounted, ref } from 'vue'
import { gsap } from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'

gsap.registerPlugin(ScrollTrigger)

const skillsRef = ref<HTMLElement>()
const skills = ref([
  {
    name: 'HTML',
    level: 90,
    logo: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/html5/html5-original.svg'
  },
  {
    name: 'CSS',
    level: 88,
    logo: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/css3/css3-original.svg'
  },
  {
    name: 'JavaScript',
    level: 85,
    logo: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/javascript/javascript-original.svg'
  },
  {
    name: 'Node.js',
    level: 80,
    logo: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/nodejs/nodejs-original.svg'
  },
  {
    name: 'Bootstrap',
    level: 80,
    logo: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/bootstrap/bootstrap-original.svg'
  },
  {
    name: 'Firebase',
    level: 90,
    logo: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/firebase/firebase-plain.svg'
  },
  {
    name: 'Git',
    level: 84,
    logo: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/git/git-original.svg'
  },
  {
    name: 'GitHub',
    level: 85,
  logo: 'https://github.githubassets.com/images/modules/logos_page/GitHub-Mark.png'
  },
  {
    name: 'Figma',
    level: 83,
    logo: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/figma/figma-original.svg'
  }
])


onMounted(() => {
  const tl = gsap.timeline({
    scrollTrigger: {
      trigger: skillsRef.value,
      start: 'top 80%',
      toggleActions: 'play none none reverse'
    }
  })
  
  tl.fromTo('.skill-item',
    { x: -100, opacity: 0, scale: 0.9 },
    { 
      x: 0, 
      opacity: 1, 
      scale: 1, 
      duration: 0.6, 
      stagger: 0.1,
      ease: 'power3.out'
    }
  )
  
  // Animate progress bars
  skills.value.forEach((skill, index) => {
    gsap.fromTo(`.progress-fill-${index}`,
      { width: '0%' },
      {
        width: `${skill.level}%`,
        duration: 1.5,
        delay: 0.2 + index * 0.1,
        ease: 'power2.out',
        scrollTrigger: {
          trigger: skillsRef.value,
          start: 'top 80%',
          toggleActions: 'play none none reverse'
        }
      }
    )
  })
})
</script>

<template>
  <section id="skills" ref="skillsRef" class="section skills">
  <div class="container">
    <h2 class="section-title text-center">
      My <span class="gradient-text">Skills</span>
    </h2>

    <div class="skills-horizontal">
      <div 
        v-for="(skill, index) in skills" 
        :key="skill.name"
        class="skill-item"
      >
        <!-- Ganti emoji dengan logo SVG -->
        <div class="skill-icon">
          <img :src="skill.logo" :alt="skill.name" width="40" height="40" />
        </div>

        <h3 class="skill-name">{{ skill.name }}</h3>
        <div class="skill-level">{{ skill.level }}%</div>
        
        <div class="progress-bar">
          <div 
            class="progress-fill"
            :style="{ width: skill.level + '%' }"
          ></div>
        </div>
      </div>
    </div>
  </div>
</section>

</template>

<style scoped>
.skills {
  background: var(--bg-darker);
}

.section-title {
  font-size: clamp(2rem, 5vw, 3rem);
  font-weight: 700;
  margin-bottom: 4rem;
}

.text-center {
  text-align: center;
}

.skills-horizontal {
  display: flex;
  flex-wrap: wrap;
  gap: 2rem;
  justify-content: center;
  margin-bottom: 4rem;
}

.skill-item {
  background: rgba(255, 255, 255, 0.05);
  backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 12px;
  padding: 2rem 1.5rem;
  text-align: center;
  min-width: 180px;
  flex: 1;
  max-width: 220px;
  transition: all 0.3s ease;
  cursor: pointer;
}

.skill-item:hover {
  transform: translateY(-10px);
  box-shadow: 0 20px 40px rgba(0, 255, 136, 0.15);
  border-color: rgba(0, 255, 136, 0.3);
}

.skill-icon {
  font-size: 2.5rem;
  margin-bottom: 1rem;
  display: block;
}

.skill-name {
  font-size: 1.1rem;
  font-weight: 600;
  margin-bottom: 0.5rem;
  color: var(--text-primary);
}

.skill-level {
  font-size: 1rem;
  font-weight: 700;
  color: var(--primary);
  font-family: 'JetBrains Mono', monospace;
  margin-bottom: 1rem;
}

.progress-bar {
  width: 100%;
  height: 6px;
  background: rgba(255, 255, 255, 0.1);
  border-radius: 3px;
  overflow: hidden;
  position: relative;
}

.progress-fill {
  height: 100%;
  background: linear-gradient(90deg, var(--primary) 0%, var(--secondary) 100%);
  border-radius: 3px;
  position: relative;
}

.progress-fill::after {
  content: '';
  position: absolute;
  top: 0;
  right: 0;
  width: 3px;
  height: 100%;
  background: rgba(255, 255, 255, 0.8);
  border-radius: 2px;
  animation: glow 2s ease-in-out infinite alternate;
}

@keyframes glow {
  from { opacity: 0.5; }
  to { opacity: 1; }
}

.skills-summary {
  margin-top: 4rem;
}

.summary-card {
  padding: 3rem;
  text-align: center;
  max-width: 600px;
  margin: 0 auto;
}

.summary-card h3 {
  font-size: 1.5rem;
  margin-bottom: 2rem;
  color: var(--primary);
}

.summary-card ul {
  list-style: none;
  text-align: left;
}

.summary-card li {
  padding: 0.8rem 0;
  color: var(--text-secondary);
  position: relative;
  padding-left: 2rem;
}

.summary-card li::before {
  content: '✓';
  position: absolute;
  left: 0;
  color: var(--primary);
  font-weight: bold;
}

@media (max-width: 768px) {
  .skills-horizontal {
    flex-direction: column;
    align-items: center;
  }
  
  .skill-item {
    max-width: 100%;
    width: 100%;
  }
  
  .summary-card {
    padding: 2rem;
  }
}

@media (max-width: 480px) {
  .skills-horizontal {
    gap: 1rem;
  }
  
  .skill-item {
    padding: 1.5rem 1rem;
    min-width: 150px;
  }
}
</style>