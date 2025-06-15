<script setup lang="ts">
import { ref, onMounted } from 'vue'
import { gsap } from 'gsap'

const isMenuOpen = ref(false)
const navRef = ref<HTMLElement>()

onMounted(() => {
  if (navRef.value) {
    gsap.fromTo(
      navRef.value,
      { y: -100, opacity: 0 },
      { y: 0, opacity: 1, duration: 1, delay: 0.5 }
    );
  }
})

const scrollToSection = (sectionId: string) => {
  const element = document.getElementById(sectionId)
  if (element) {
    element.scrollIntoView({ behavior: 'smooth' })
  }
  isMenuOpen.value = false
}
</script>

<template>
  <nav ref="navRef" class="nav">
    <div class="container">
      <div class="nav-content">
        <div class="logo">
          <span class="gradient-text">ZMR</span>
        </div>
        
        <div class="nav-links" :class="{ 'nav-open': isMenuOpen }">
          <a @click="scrollToSection('hero')" class="nav-link">Home</a>
          <a @click="scrollToSection('about')" class="nav-link">About</a>
          <a @click="scrollToSection('skills')" class="nav-link">Skills</a>
          <a @click="scrollToSection('projects')" class="nav-link">Projects</a>
          <a @click="scrollToSection('contact')" class="nav-link">Contact</a>
        </div>
        
        <button 
          class="menu-toggle"
          @click="isMenuOpen = !isMenuOpen"
          :class="{ 'menu-open': isMenuOpen }"
        >
          <span></span>
          <span></span>
          <span></span>
        </button>
      </div>
    </div>
  </nav>
</template>

<style scoped>
.nav {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 1000;
  padding: 1rem 0;
  background: rgba(10, 10, 10, 0.9);
  backdrop-filter: blur(20px);
  border-bottom: 1px solid rgba(255, 255, 255, 0.1);
}

.nav-content {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.logo {
  font-size: 1.5rem;
  font-weight: 700;
  font-family: 'JetBrains Mono', monospace;
}

.nav-links {
  display: flex;
  gap: 2rem;
  list-style: none;
}

.nav-link {
  color: var(--text-secondary);
  text-decoration: none;
  font-weight: 500;
  cursor: pointer;
  transition: all 0.3s ease;
  position: relative;
  padding: 0.5rem 0;
}

.nav-link:hover {
  color: var(--primary);
}

.nav-link::after {
  content: '';
  position: absolute;
  bottom: 0;
  left: 0;
  width: 0;
  height: 2px;
  background: var(--primary);
  transition: width 0.3s ease;
}

.nav-link:hover::after {
  width: 100%;
}

.menu-toggle {
  display: none;
  flex-direction: column;
  gap: 4px;
  background: none;
  border: none;
  cursor: pointer;
  padding: 8px;
}

.menu-toggle span {
  width: 25px;
  height: 2px;
  background: var(--text-primary);
  transition: all 0.3s ease;
}

/* Tablet Styles */
@media (max-width: 1024px) {
  .nav-links {
    gap: 1.5rem;
  }
  
  .nav-link {
    font-size: 0.95rem;
  }
}

/* Mobile Styles */
@media (max-width: 768px) {
  .nav {
    padding: 0.8rem 0;
  }
  
  .nav-links {
    position: fixed;
    top: 70px;
    left: 0;
    right: 0;
    background: rgba(10, 10, 10, 0.95);
    backdrop-filter: blur(20px);
    flex-direction: column;
    padding: 2rem;
    transform: translateY(-100%);
    opacity: 0;
    visibility: hidden;
    transition: all 0.3s ease;
    border-bottom: 1px solid rgba(255, 255, 255, 0.1);
  }
  
  .nav-open {
    transform: translateY(0);
    opacity: 1;
    visibility: visible;
  }
  
  .nav-link {
    padding: 1rem 0;
    font-size: 1.1rem;
    text-align: center;
    border-bottom: 1px solid rgba(255, 255, 255, 0.1);
  }
  
  .nav-link:last-child {
    border-bottom: none;
  }
  
  .menu-toggle {
    display: flex;
  }
  
  .menu-open span:nth-child(1) {
    transform: rotate(45deg) translate(6px, 6px);
  }
  
  .menu-open span:nth-child(2) {
    opacity: 0;
  }
  
  .menu-open span:nth-child(3) {
    transform: rotate(-45deg) translate(6px, -6px);
  }
  
  .logo {
    font-size: 1.3rem;
  }
}

/* Small Mobile Styles */
@media (max-width: 480px) {
  .nav {
    padding: 0.6rem 0;
  }
  
  .nav-links {
    top: 60px;
    padding: 1.5rem;
  }
  
  .nav-link {
    padding: 0.8rem 0;
    font-size: 1rem;
  }
  
  .logo {
    font-size: 1.2rem;
  }
}
</style>