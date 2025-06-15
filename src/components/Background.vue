<script setup lang="ts">
import { onMounted, ref } from 'vue'
import { gsap } from 'gsap'

const backgroundRef = ref<HTMLElement>()
const particles = ref<Array<{ x: number; y: number; vx: number; vy: number }>>([])

onMounted(() => {
  // Create floating particles
  for (let i = 0; i < 50; i++) {
    particles.value.push({
      x: Math.random() * window.innerWidth,
      y: Math.random() * window.innerHeight,
      vx: (Math.random() - 0.5) * 0.5,
      vy: (Math.random() - 0.5) * 0.5
    })
  }
  
  // Animate particles
  const animateParticles = () => {
    particles.value.forEach((particle, i) => {
      particle.x += particle.vx
      particle.y += particle.vy
      
      if (particle.x < 0 || particle.x > window.innerWidth) particle.vx *= -1
      if (particle.y < 0 || particle.y > window.innerHeight) particle.vy *= -1
      
      const element = document.getElementById(`particle-${i}`)
      if (element) {
        gsap.set(element, { x: particle.x, y: particle.y })
      }
    })
    requestAnimationFrame(animateParticles)
  }
  
  animateParticles()
  
  // Mouse follower effect
  const handleMouseMove = (e: MouseEvent) => {
    gsap.to('.mouse-follower', {
      x: e.clientX,
      y: e.clientY,
      duration: 0.8,
      ease: 'power2.out'
    })
  }
  
  document.addEventListener('mousemove', handleMouseMove)
})
</script>

<template>
  <div ref="backgroundRef" class="background">
    <div class="gradient-overlay"></div>
    <div class="particles">
      <div 
        v-for="(particle, i) in particles" 
        :key="i"
        :id="`particle-${i}`"
        class="particle"
      ></div>
    </div>
    <div class="mouse-follower"></div>
  </div>
</template>

<style scoped>
.background {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: -1;
  overflow: hidden;
}

.gradient-overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: radial-gradient(
    circle at 20% 50%,
    rgba(0, 255, 136, 0.1) 0%,
    transparent 50%
  ),
  radial-gradient(
    circle at 80% 20%,
    rgba(0, 102, 255, 0.1) 0%,
    transparent 50%
  ),
  radial-gradient(
    circle at 40% 80%,
    rgba(255, 107, 107, 0.1) 0%,
    transparent 50%
  );
}

.particles {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}

.particle {
  position: absolute;
  width: 2px;
  height: 2px;
  background: var(--primary);
  border-radius: 50%;
  opacity: 0.3;
  filter: blur(0.5px);
}

.mouse-follower {
  position: absolute;
  width: 20px;
  height: 20px;
  background: radial-gradient(circle, var(--primary) 0%, transparent 70%);
  border-radius: 50%;
  pointer-events: none;
  opacity: 0.3;
  filter: blur(10px);
}
</style>