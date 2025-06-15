<script setup lang="ts">
import { onMounted, ref } from 'vue'
import { gsap } from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'

gsap.registerPlugin(ScrollTrigger)

const contactRef = ref<HTMLElement>()
const formRef = ref<HTMLElement>()
const infoRef = ref<HTMLElement>()

const form = ref({
  name: '',
  email: '',
  message: ''
})

onMounted(() => {
  const tl = gsap.timeline({
    scrollTrigger: {
      trigger: contactRef.value,
      start: 'top 80%',
      toggleActions: 'play none none reverse'
    }
  });

  if (infoRef.value) {
    tl.fromTo(
      infoRef.value,
      { x: -100, opacity: 0 },
      { x: 0, opacity: 1, duration: 1, ease: 'power3.out' }
    );
  }

  if (formRef.value) {
    tl.fromTo(
      formRef.value,
      { x: 100, opacity: 0 },
      { x: 0, opacity: 1, duration: 1, ease: 'power3.out' },
      '-=0.8'
    );
  }
})

const handleSubmit = (e: Event) => {
  e.preventDefault()
  // Handle form submission here
  console.log('Form submitted:', form.value)

  // Reset form
  form.value = {
    name: '',
    email: '',
    message: ''
  }

  // Show success message (you can implement this)
  alert('Message sent successfully! I\'ll get back to you soon.')
}
</script>

<template>
  <section id="contact" ref="contactRef" class="section contact">
    <div class="container">
      <div class="contact-header">
        <h2 class="section-title">
          Get In <span class="gradient-text">Touch</span>
        </h2>
        <p class="section-subtitle">
          Ready to bring your ideas to life? Let's create something amazing together.
        </p>
      </div>

      <div class="contact-grid">
        <div ref="infoRef" class="contact-info">
          <div class="info-card glass">
            <div class="info-header">
              <div class="header-icon">💬</div>
              <h3>Let's Start a Conversation</h3>
            </div>

            <p class="info-description">
              I'm always excited to work on new projects and collaborate with creative minds.
              Whether you have a project in mind or just want to say hello, I'd love to hear from you!
            </p>

            <div class="contact-methods">
              <div class="contact-method">
                <div class="method-icon email-icon">
                  <svg width="20" height="20" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <path
                      d="M4 4H20C21.1 4 22 4.9 22 6V18C22 19.1 21.1 20 20 20H4C2.9 20 2 19.1 2 18V6C2 4.9 2.9 4 4 4Z"
                      stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" />
                    <polyline points="22,6 12,13 2,6" stroke="currentColor" stroke-width="2" stroke-linecap="round"
                      stroke-linejoin="round" />
                  </svg>
                </div>
                <div class="method-content">
                  <h4>Email</h4>
                  <p>ziikran123@gmail.com</p>
                </div>
              </div>

              <div class="contact-method">
                <div class="method-icon phone-icon">
                  <svg width="20" height="20" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <path
                      d="M22 16.92V19.92C22 20.52 21.39 21 20.77 21C9.39 21 0 11.61 0 0.23C0 -0.39 0.48 -1 1.08 -1H4.08C4.68 -1 5.08 -0.39 5.08 0.23C5.08 2.23 5.48 4.23 6.28 6.03C6.48 6.43 6.38 6.93 6.08 7.23L4.08 9.23C5.68 12.43 8.57 15.32 11.77 16.92L13.77 14.92C14.07 14.62 14.57 14.52 14.97 14.72C16.77 15.52 18.77 15.92 20.77 15.92C21.39 15.92 22 16.4 22 16.92Z"
                      stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" />
                  </svg>
                </div>
                <div class="method-content">
                  <h4>Phone</h4>
                  <p>+62 819 0880 3875</p>
                </div>
              </div>

              <div class="contact-method">
                <div class="method-icon location-icon">
                  <svg width="20" height="20" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <path d="M21 10C21 17 12 23 12 23S3 17 3 10C3 5.03 7.03 1 12 1S21 5.03 21 10Z" stroke="currentColor"
                      stroke-width="2" stroke-linecap="round" stroke-linejoin="round" />
                    <circle cx="12" cy="10" r="3" stroke="currentColor" stroke-width="2" stroke-linecap="round"
                      stroke-linejoin="round" />
                  </svg>
                </div>
                <div class="method-content">
                  <h4>Location</h4>
                  <p>Tangerang Selatan, Indonesia</p>
                </div>
              </div>
            </div>

            <div class="social-section">
              <h4>Follow Me</h4>
              <div class="social-links">
                <a href="https://www.linkedin.com/in/muhammad-zikran" class="social-link linkedin">
                  <svg width="20" height="20" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <path
                      d="M16 8C17.5913 8 19.1174 8.63214 20.2426 9.75736C21.3679 10.8826 22 12.4087 22 14V21H18V14C18 13.4696 17.7893 12.9609 17.4142 12.5858C17.0391 12.2107 16.5304 12 16 12C15.4696 12 14.9609 12.2107 14.5858 12.5858C14.2107 12.9609 14 13.4696 14 14V21H10V14C10 12.4087 10.6321 10.8826 11.7574 9.75736C12.8826 8.63214 14.4087 8 16 8Z"
                      stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" />
                    <path d="M6 9H2V21H6V9Z" stroke="currentColor" stroke-width="2" stroke-linecap="round"
                      stroke-linejoin="round" />
                    <path
                      d="M4 6C5.10457 6 6 5.10457 6 4C6 2.89543 5.10457 2 4 2C2.89543 2 2 2.89543 2 4C2 5.10457 2.89543 6 4 6Z"
                      stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" />
                  </svg>
                  <span>LinkedIn</span>
                </a>
                <a href="https://github.com/zikran11" class="social-link github">
                  <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="black">
                    <path
                      d="M12 .5C5.65.5.5 5.65.5 12c0 5.1 3.3 9.4 7.9 10.9.6.1.8-.3.8-.6v-2c-3.2.7-3.8-1.5-3.8-1.5-.5-1.2-1.2-1.5-1.2-1.5-1-.6.1-.6.1-.6 1.1.1 1.7 1.1 1.7 1.1 1 .1.8-.8.8-.8-.6-1.1-.8-1.6-.8-2.3 0-2 .8-3 2.2-3.6-.3-.6-.6-1.5-.2-2.5 0 0 1.1-.3 3.6 1.4 1-.3 2.1-.5 3.2-.5s2.2.2 3.2.5c2.5-1.7 3.6-1.4 3.6-1.4.3 1 .1 1.9-.2 2.5 1.4.6 2.2 1.6 2.2 3.6 0 .7-.2 1.3-.8 2.3 0 0 .2.9.8.8 0 0 .6-1 1.7-1.1 0 0 1.1 0 .1.6 0 0-.7.3-1.2 1.5 0 0-.6 2.2-3.8 1.5v2c0 .3.2.7.8.6C20.7 21.4 24 17.1 24 12c0-6.35-5.15-11.5-12-11.5z" />
                  </svg>
                  <span>GitHub</span>
                </a>
              </div>
            </div>
          </div>
        </div>

        <div ref="formRef" class="contact-form">
          <div class="form-container glass">
            <div class="form-header">
              <h3>Send Me a Message</h3>
              <p>Fill out the form below and I'll get back to you as soon as possible.</p>
            </div>

            <form @submit="handleSubmit" class="form">
              <div class="form-row">
                <div class="form-group">
                  <label for="name">Full Name</label>
                  <input type="text" id="name" v-model="form.name" required placeholder="Zikran" />
                </div>

                <div class="form-group">
                  <label for="email">Email Address</label>
                  <input type="email" id="email" v-model="form.email" required placeholder="zik@example.com" />
                </div>
              </div>

              <div class="form-group">
                <label for="message">Your Message</label>
                <textarea id="message" v-model="form.message" required rows="6"
                  placeholder="Tell me about your project, ideas, or just say hello! I'd love to hear from you."></textarea>
              </div>

              <button type="submit" class="submit-btn">
                <span>Send Message</span>
                <svg width="16" height="16" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                  <path d="M22 2L11 13" stroke="currentColor" stroke-width="2" stroke-linecap="round"
                    stroke-linejoin="round" />
                  <path d="M22 2L15 22L11 13L2 9L22 2Z" stroke="currentColor" stroke-width="2" stroke-linecap="round"
                    stroke-linejoin="round" />
                </svg>
              </button>
            </form>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.contact {
  background: linear-gradient(135deg, var(--bg-darker) 0%, rgba(0, 102, 255, 0.03) 50%, var(--bg-darker) 100%);
  padding: 6rem 0 0;
}

.contact-header {
  text-align: center;
  margin-bottom: 5rem;
}

.section-title {
  font-size: clamp(2.5rem, 6vw, 4rem);
  font-weight: 700;
  margin-bottom: 1.5rem;
  line-height: 1.2;
}

.section-subtitle {
  font-size: clamp(1.1rem, 2.5vw, 1.3rem);
  color: var(--text-secondary);
  max-width: 600px;
  margin: 0 auto;
  line-height: 1.6;
}

.contact-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 4rem;
  margin-bottom: 4rem;
  align-items: start;
}

.info-card {
  padding: 3rem;
  height: fit-content;
  position: sticky;
  top: 2rem;
}

.info-header {
  display: flex;
  align-items: center;
  gap: 1rem;
  margin-bottom: 2rem;
}

.header-icon {
  font-size: 2rem;
  width: 3.5rem;
  height: 3.5rem;
  display: flex;
  align-items: center;
  justify-content: center;
  background: linear-gradient(135deg, var(--primary), var(--secondary));
  border-radius: 15px;
}

.info-header h3 {
  font-size: 1.8rem;
  font-weight: 700;
  color: var(--text-primary);
}

.info-description {
  color: var(--text-secondary);
  line-height: 1.8;
  margin-bottom: 3rem;
  font-size: 1.05rem;
}

.contact-methods {
  margin-bottom: 3rem;
}

.contact-method {
  display: flex;
  align-items: center;
  gap: 1.2rem;
  margin-bottom: 2rem;
  padding: 1rem;
  border-radius: 12px;
  transition: all 0.3s ease;
}

.contact-method:hover {
  background: rgba(0, 255, 136, 0.05);
  transform: translateX(5px);
}

.method-icon {
  width: 3rem;
  height: 3rem;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 10px;
  color: var(--primary);
  transition: all 0.3s ease;
}

.email-icon {
  background: rgba(0, 255, 136, 0.1);
}

.phone-icon {
  background: rgba(0, 102, 255, 0.1);
}

.location-icon {
  background: rgba(255, 107, 107, 0.1);
}

.method-content h4 {
  margin-bottom: 0.3rem;
  font-weight: 600;
  color: var(--text-primary);
}

.method-content p {
  color: var(--text-secondary);
  margin: 0;
  font-size: 0.95rem;
}

.social-section {
  border-top: 1px solid rgba(255, 255, 255, 0.1);
  padding-top: 2rem;
}

.social-section h4 {
  margin-bottom: 1.5rem;
  color: var(--text-primary);
  font-weight: 600;
}

.social-links {
  display: flex;
  flex-direction: column;
  gap: 0.8rem;
}

.social-link {
  display: flex;
  align-items: center;
  gap: 0.8rem;
  padding: 0.8rem 1rem;
  background: rgba(255, 255, 255, 0.03);
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 10px;
  color: var(--text-secondary);
  text-decoration: none;
  transition: all 0.3s ease;
  font-weight: 500;
}

.social-link:hover {
  transform: translateY(-2px);
  box-shadow: 0 8px 25px rgba(0, 255, 136, 0.15);
}

.social-link.linkedin:hover {
  border-color: #0077b5;
  color: #0077b5;
}

.social-link.github:hover {
  border-color: var(--text-primary);
  color: var(--text-primary);
}

.social-link.twitter:hover {
  border-color: #1da1f2;
  color: #1da1f2;
}

.form-container {
  padding: 3rem;
}

.form-header {
  margin-bottom: 2.5rem;
}

.form-header h3 {
  font-size: 1.6rem;
  font-weight: 700;
  margin-bottom: 0.8rem;
  color: var(--text-primary);
}

.form-header p {
  color: var(--text-secondary);
  line-height: 1.6;
}

.form-row {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 1.5rem;
  margin-bottom: 2rem;
}

.form-group {
  margin-bottom: 2rem;
}

.form-group label {
  display: block;
  margin-bottom: 0.8rem;
  font-weight: 600;
  color: var(--text-primary);
  font-size: 0.95rem;
}

.form-group input,
.form-group textarea {
  width: 100%;
  padding: 1.2rem;
  background: rgba(255, 255, 255, 0.05);
  border: 2px solid rgba(255, 255, 255, 0.1);
  border-radius: 12px;
  color: var(--text-primary);
  font-size: 1rem;
  transition: all 0.3s ease;
  font-family: inherit;
}

.form-group input:focus,
.form-group textarea:focus {
  outline: none;
  border-color: var(--primary);
  box-shadow: 0 0 0 3px rgba(0, 255, 136, 0.1);
  background: rgba(255, 255, 255, 0.08);
}

.form-group input::placeholder,
.form-group textarea::placeholder {
  color: var(--text-secondary);
  opacity: 0.7;
}

.form-group textarea {
  resize: vertical;
  min-height: 120px;
}

.submit-btn {
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.8rem;
  padding: 1.3rem 2rem;
  background: linear-gradient(135deg, var(--primary) 0%, var(--secondary) 100%);
  border: none;
  border-radius: 12px;
  color: var(--bg-dark);
  font-weight: 700;
  font-size: 1.05rem;
  cursor: pointer;
  transition: all 0.3s ease;
  position: relative;
  overflow: hidden;
}

.submit-btn:hover {
  transform: translateY(-2px);
  box-shadow: 0 15px 35px rgba(0, 255, 136, 0.3);
}

.submit-btn:active {
  transform: translateY(0);
}

.footer {
  background: rgba(0, 0, 0, 0.3);
  border-top: 1px solid rgba(255, 255, 255, 0.1);
  padding: 3rem 0;
  margin-top: 4rem;
}

.footer-content {
  text-align: center;
}

.footer-content p {
  color: var(--text-secondary);
  margin-bottom: 0.5rem;
}

.footer-tagline {
  font-size: 0.9rem;
  opacity: 0.8;
}

/* Tablet Styles */
@media (max-width: 1024px) {
  .contact {
    padding: 4rem 0 0;
  }

  .contact-grid {
    gap: 3rem;
  }

  .info-card,
  .form-container {
    padding: 2.5rem;
  }

  .section-title {
    font-size: clamp(2rem, 5vw, 3rem);
  }
}

/* Mobile Styles */
@media (max-width: 768px) {
  .contact {
    padding: 3rem 0 0;
  }

  .contact-header {
    margin-bottom: 3rem;
  }

  .contact-grid {
    grid-template-columns: 1fr;
    gap: 2rem;
  }

  .info-card {
    position: static;
    padding: 2rem;
  }

  .form-container {
    padding: 2rem;
  }

  .form-row {
    grid-template-columns: 1fr;
    gap: 0;
  }

  .social-links {
    flex-direction: row;
    flex-wrap: wrap;
    gap: 0.5rem;
  }

  .social-link {
    flex: 1;
    min-width: 120px;
    justify-content: center;
  }

  .contact-method {
    padding: 0.8rem;
  }

  .method-icon {
    width: 2.5rem;
    height: 2.5rem;
  }
}

/* Small Mobile Styles */
@media (max-width: 480px) {
  .contact {
    padding: 2rem 0 0;
  }

  .info-card,
  .form-container {
    padding: 1.5rem;
  }

  .info-header {
    flex-direction: column;
    text-align: center;
    gap: 0.8rem;
  }

  .header-icon {
    width: 3rem;
    height: 3rem;
  }

  .contact-method {
    flex-direction: column;
    text-align: center;
    gap: 0.8rem;
  }

  .social-links {
    flex-direction: column;
  }

  .social-link {
    min-width: auto;
  }

  .form-group input,
  .form-group textarea {
    padding: 1rem;
  }

  .submit-btn {
    padding: 1.2rem;
    font-size: 1rem;
  }
}
</style>