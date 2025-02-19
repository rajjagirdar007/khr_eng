<!-- App.vue -->
<template>
  <div class="app-container">
    <!-- Enhanced Navbar with Backdrop Blur -->
    <nav class="nav" :class="{ 'nav-scrolled': isScrolled }">
      <div class="nav-inner">
        <div class="logo">
          <svg xmlns="http://www.w3.org/2000/svg"   
          width="60"
          height="70">
            <!-- Simple geometric shape representing a K with an integrated H -->
            <path 
              d="
                M 10,10 
                L 10,60 
                L 18,60 
                L 18,40 
                L 30,60 
                L 40,60 
                L 28,35 
                L 40,10 
                L 30,10 
                L 18,32 
                L 18,10 
                L 10,10 
                Z
                M 45,10 
                L 45,60 
                L 53,60 
                L 53,10 
                L 45,10
                Z
                M 18,32
                L 45,32
                L 45,40
                L 18,40
                Z
              "
            />
            <!-- Subtle dot representing the R -->
            <circle cx="49" cy="22" r="3" />
          </svg>
        </div>
        <div class="nav-links">
          <a
            v-for="link in navLinks"
            :key="link.id"
            :href="link.path"
            class="nav-link"
            :class="{ 'nav-link-active': activeSection === link.path.slice(1) }"
            @click.prevent="scrollToSection(link.path)"
          >
            {{ link.name }}
          </a>
        </div>
      </div>
    </nav>

    <!-- Refined Hero Section with Gradient Background -->
    <section class="hero" id="home" v-intersect="onIntersect">
      <div class="hero-content" :class="{ 'fade-in-up': isVisible }">
        <h1 class="hero-title">
          Revolutionizing
          <span class="gradient-text">Civil Engineering</span>
        </h1>
        <p class="hero-subtitle">
          Merging traditional excellence with innovative technology.
        </p>
        <div class="hero-cta">
          <button class="btn primary"  @click.prevent="scrollToSection('#services')">
            Explore Solutions
            <span class="btn-arrow">→</span>
          </button>
          <button class="btn secondary"  @click.prevent="scrollToSection('#projects')">View Projects</button>
        </div>
      </div>
      <div class="hero-background">
        <div class="gradient-sphere"></div>
      </div>
    </section>

    <!-- Enhanced Services Section -->
    <section class="services" id="services" v-intersect="onIntersect">
      <div class="section-container">
        <h2 class="section-title" :class="{ 'fade-in-up': isVisible }">
          Our Expertise
        </h2>
        <div class="services-grid">
          <div
            v-for="(service, index) in services"
            :key="service.id"
            class="service-card"
            :class="{ 'fade-in-up': isVisible }"
            :style="{ animationDelay: index * 0.2 + 's' }"
          >
            <div class="service-icon">
              <component :is="service.icon" />
            </div>
            <h3 class="service-title">{{ service.title }}</h3>
            <p class="service-description">{{ service.description }}</p>
          </div>
        </div>
      </div>
    </section>

    <!-- Refined Projects Section -->
    <section class="projects" id="projects" v-intersect="onIntersect">
      <div class="section-container">
        <h2 class="section-title" :class="{ 'fade-in-up': isVisible }">
          Featured Projects
        </h2>
        <div class="projects-grid">
          <div
            v-for="(project, index) in projects"
            :key="project.id"
            class="project-card"
            :class="{ 'fade-in-up': isVisible }"
            :style="{ animationDelay: index * 0.2 + 's' }"
          >
            <div class="project-image">
              <img :src="project.image" :alt="project.title" />
            </div>
            <div class="project-content">
              <h3 class="project-title">{{ project.title }}</h3>
              <p class="project-description">{{ project.description }}</p>
              <button class="btn text">
                Learn more
                <span class="btn-arrow">→</span>
              </button>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Enhanced Software Section -->
    <section class="software" id="software" v-intersect="onIntersect">
      <div class="section-container">
        <h2 class="section-title" :class="{ 'fade-in-up': isVisible }">
          Software Solutions
        </h2>
        <div class="software-grid">
          <div
            v-for="(solution, index) in softwareSolutions"
            :key="solution.id"
            class="software-card"
            :class="{ 'fade-in-up': isVisible }"
            :style="{ animationDelay: index * 0.2 + 's' }"
          >
            <div class="software-icon">
              <component :is="solution.icon" />
            </div>
            <h3 class="software-title">{{ solution.title }}</h3>
            <p class="software-description">{{ solution.description }}</p>
            <button class="btn text">
              Explore Features
              <span class="btn-arrow">→</span>
            </button>
          </div>
        </div>
      </div>
    </section>

    <!-- Refined Contact Section -->
    <section class="contact" id="contact" v-intersect="onIntersect">
      <div class="contact-inner">
        <div class="contact-content" :class="{ 'fade-in-up': isVisible }">
          <h2 class="contact-title">Let's Build Together</h2>
          <p class="contact-subtitle">Transform your vision into reality</p>
          <form @submit.prevent="handleSubmit" class="contact-form">
            <div class="form-group">
              <input 
                type="text" 
                v-model="form.name" 
                placeholder="Your Name" 
                required
                aria-label="Your Name"
              />
            </div>
            <div class="form-group">
              <input 
                type="email" 
                v-model="form.email" 
                placeholder="Your Email" 
                required
                aria-label="Your Email"
              />
            </div>
            <div class="form-group">
              <textarea 
                v-model="form.message" 
                placeholder="Project Details" 
                required
                aria-label="Project Details"
              ></textarea>
            </div>
            <button type="submit" class="btn primary">
              Start Your Project
              <span class="btn-arrow">→</span>
            </button>
          </form>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
import { Building2, Bridge, Code2, Layout, Database, Cpu, Construction } from 'lucide-vue-next';

export default {
  name: "App",
  data() {
    return {
      isScrolled: false,
      activeSection: '',
      isVisible: false,
      navLinks: [
        { id: 1, name: "Services", path: "#services" },
        { id: 2, name: "Projects", path: "#projects" },
        { id: 3, name: "Software", path: "#software" },
        { id: 4, name: "Contact", path: "#contact" },
      ],
      services: [
        { 
          id: 1, 
          title: "Structural Engineering", 
          description: "Precision, safety, and efficiency in design.",
          icon: Building2
        },
        { 
          id: 2, 
          title: "Infrastructure Design", 
          description: "Innovative solutions for modern cities.",
          icon: Construction
        },
        { 
          id: 3, 
          title: "Engineering Software", 
          description: "Cutting-edge tools for optimal performance.",
          icon: Code2
        },
      ],
      projects: [
        { 
          id: 1, 
          title: "Smart City Infrastructure", 
          description: "A revolutionary urban project integrating sustainable technologies and innovative design principles.",
          image: "https://images.pexels.com/photos/599982/pexels-photo-599982.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=2"
        },
        { 
          id: 2, 
          title: "Sustainable Bridge Design", 
          description: "An award-winning bridge design that combines architectural beauty with environmental consciousness.",
          image: "https://images.pexels.com/photos/220762/pexels-photo-220762.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=2"
        },
      ],
      softwareSolutions: [
        { 
          id: 1, 
          title: "BIM Integration Platform", 
          description: "Seamless collaboration platform for building information modeling and design optimization.",
          icon: Layout
        },
        { 
          id: 2, 
          title: "Structural Analysis Suite", 
          description: "Advanced analytics toolkit powered by machine learning for precise structural calculations.",
          icon: Database
        },
        { 
          id: 3, 
          title: "Smart Infrastructure Monitor", 
          description: "Real-time monitoring and predictive maintenance system for infrastructure assets.",
          icon: Cpu
        },
      ],
      form: {
        name: "",
        email: "",
        message: ""
      }
    };
  },
  mounted() {
    window.addEventListener('scroll', this.handleScroll);
    this.handleScroll();
  },
  beforeDestroy() {
    window.removeEventListener('scroll', this.handleScroll);
  },
  methods: {
    scrollToSection(path) {
      const element = document.querySelector(path);
      if (element) {
        element.scrollIntoView({ 
          behavior: 'smooth',
          block: 'start'
        });
        this.activeSection = path.slice(1);
      }
    },
    handleScroll() {
      this.isScrolled = window.scrollY > 50;
      
      // Update active section based on scroll position
      const sections = ['services', 'projects', 'software', 'contact'];
      for (const section of sections) {
        const element = document.getElementById(section);
        if (element) {
          const rect = element.getBoundingClientRect();
          if (rect.top <= 100 && rect.bottom >= 100) {
            this.activeSection = section;
            break;
          }
        }
      }
    },
    handleSubmit() {
      console.log("Form submitted", this.form);
      // Add form submission logic here
    },
    onIntersect(entries) {
      this.isVisible = entries[0].isIntersecting;
    }
  }
};
</script>

<style>
/* Base Styles & Typography */
:root {
  --primary-color: #0066CC;
  --secondary-color: #86868b;
  --background-light: #fbfbfd;
  --text-primary: #1d1d1f;
  --text-secondary: #6e6e73;
  --spacing-xs: 0.5rem;
  --spacing-sm: 1rem;
  --spacing-md: 2rem;
  --spacing-lg: 4rem;
  --border-radius: 1rem;
  --transition-fast: 0.2s ease;
  --transition-smooth: 0.3s cubic-bezier(0.4, 0, 0.2, 1);
}

body {
  margin: 0;
  font-family: -apple-system, BlinkMacSystemFont, "SF Pro Display", "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  background: var(--background-light);
  color: var(--text-primary);
  line-height: 1.5;
}

.app-container {
  overflow-x: hidden;
}

/* Enhanced Navigation */
.nav {
  position: fixed;
  top: 0;
  width: 100%;
  background: rgba(255, 255, 255, 0.8);
  backdrop-filter: blur(20px);
  -webkit-backdrop-filter: blur(20px);
  transition: all var(--transition-smooth);
  z-index: 1000;
}

.nav-scrolled {
  background: rgba(255, 255, 255, 0.95);
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
}

.nav-inner {
  max-width: 1200px;
  margin: 0 auto;
  padding: var(--spacing-sm) var(--spacing-md);
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.logo-image {
  width: 32px;
  height: 40px;
  transition: transform var(--transition-fast);
}

.logo-image:hover {
  transform: scale(1.05);
}

.nav-links {
  display: flex;
  gap: var(--spacing-md);
}

.nav-link {
  text-decoration: none;
  color: var(--text-primary);
  font-weight: 500;
  transition: all var(--transition-smooth);
  position: relative;
  padding: var(--spacing-xs) 0;
}

.nav-link::after {
  content: '';
  position: absolute;
  bottom: 0;
  left: 0;
  width: 0;
  height: 2px;
  background: var(--primary-color);
  transition: width var(--transition-smooth);
}

.nav-link:hover::after,
.nav-link-active::after {
  width: 100%;
}

/* Refined Hero Section */
.hero {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: calc(var(--spacing-lg) * 2) var(--spacing-md);
  text-align: center;
  position: relative;
  overflow: hidden;
  min-height: 50vh;
  justify-content: center;
}

.hero-content {
  max-width: 800px;
  margin-bottom: var(--spacing-md);
  position: relative;
  z-index: 2;
}

.hero-title {
  font-size: 4rem;
  font-weight: 700;
  margin: 0 0 var(--spacing-sm);
  line-height: 1.1;
}

.gradient-text {
  background: linear-gradient(135deg, var(--primary-color), #00a0ff);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.hero-subtitle {
  font-size: 1.5rem;
  margin: 0 0 var(--spacing-md);
  color: var(--text-secondary);
}

.hero-background {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 1;
}

.gradient-sphere {
  position: absolute;
  width: 600px;
  height: 600px;
  background: radial-gradient(circle, rgba(0, 102, 204, 0.1) 0%, rgba(0, 102, 204, 0) 70%);
  border-radius: 50%;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}

/* Enhanced Buttons */
.btn {
  padding: 0.875rem 1.75rem;
  font-size: 1rem;
  border: none;
  border-radius: 2rem;
  cursor: pointer;
  font-weight: 500;
  transition: all var(--transition-smooth);
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
  margin: .5rem
}

.btn-arrow {
  transition: transform var(--transition-smooth);
}

.btn:hover .btn-arrow {
  transform: translateX(4px);
}

.btn.primary {
  background: var(--primary-color);
  color: white;
}

.btn.primary:hover {
  transform: translateY(-2px);
  box-shadow: 0 4px 12px rgba(0, 102, 204, 0.3);
}

.btn.secondary {
  background: transparent;
  color: var(--primary-color);
  border: 1px solid var(--primary-color);
}

.btn.secondary:hover {
  background: rgba(0, 102, 204, 0.05);
  transform: translateY(-2px);
}

.btn.text {
  background: transparent;
  color: var(--primary-color);
  padding: var(--spacing-xs) 0;
}

.btn.text:hover {
  color: #0052a3;
}

.btn.text-small {
  font-size: 0.875rem;
  padding: var(--spacing-xs) 0;
}

/* Section Containers */
.section-container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 var(--spacing-md);
}

/* Refined Section Titles */
.section-title {
  font-size: 2.5rem;
  text-align: center;
  margin: 0 0 var(--spacing-lg);
  font-weight: 600;
  color: var(--text-primary);
}

/* Enhanced Services Section */
.services {
  padding: var(--spacing-lg) 0;
  background: white;
}

.services-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: var(--spacing-md);
  margin: 0 auto;
}

.service-card {
  padding: var(--spacing-md);
  border-radius: var(--border-radius);
  background: white;
  transition: all var(--transition-smooth);
  border: 1px solid rgba(0, 0, 0, 0.1);
}

.service-card:hover {
  transform: translateY(-4px);
  box-shadow: 0 12px 24px rgba(0, 0, 0, 0.05);
}

.service-icon {
  color: var(--primary-color);
  margin-bottom: var(--spacing-sm);
}

.service-title {
  font-size: 1.25rem;
  margin: 0 0 var(--spacing-xs);
  font-weight: 600;
}

.service-description {
  color: var(--text-secondary);
  margin: 0;
  line-height: 1.6;
}

/* Refined Projects Section */
.projects {
  padding: var(--spacing-lg) 0;
  background: var(--background-light);
}

.projects-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
  gap: var(--spacing-md);
}

.project-card {
  background: white;
  border-radius: var(--border-radius);
  overflow: hidden;
  transition: all var(--transition-smooth);
  border: 1px solid rgba(0, 0, 0, 0.1);
}

.project-card:hover {
  transform: translateY(-4px);
  box-shadow: 0 12px 24px rgba(0, 0, 0, 0.05);
}

.project-image {
  width: 100%;
  height: 240px;
  overflow: hidden;
}

.project-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform var(--transition-smooth);
}

.project-card:hover .project-image img {
  transform: scale(1.05);
}

.project-content {
  padding: var(--spacing-md);
}

.project-title {
  font-size: 1.25rem;
  margin: 0 0 var(--spacing-xs);
  font-weight: 600;
}

.project-description {
  color: var(--text-secondary);
  margin: 0 0 var(--spacing-sm);
  line-height: 1.6;
}

/* Enhanced Software Section */
/* Enhanced Software Section */
.software {
  padding: var(--spacing-lg) 0;
  background: #fff;
}

.section-container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 var(--spacing-md);
}

.section-title {
  font-size: 2rem;
  font-weight: 600;
  text-align: center;
  margin-bottom: var(--spacing-lg);
  font-family: "Montserrat", sans-serif;
  opacity: 0;
  animation: fadeInUp 0.6s ease-out forwards;
}

.software-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: var(--spacing-md);
}

.software-card {
  padding: var(--spacing-md);
  border-radius: var(--border-radius);
  background: #fff;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
  border: 1px solid rgba(0, 0, 0, 0.08);
  display: flex;
  flex-direction: column;
  opacity: 0;
  animation: fadeInUp 0.6s ease-out forwards;
}

.software-card:hover {
  transform: translateY(-6px) scale(1.02);
  box-shadow: 0 12px 24px rgba(0, 0, 0, 0.08);
}

.software-icon {
  font-size: 2rem;
  color: var(--primary-color);
  margin-bottom: var(--spacing-sm);
}

.software-title {
  font-size: 1.5rem;
  margin: 0 0 var(--spacing-xs);
  font-weight: 600;
  font-family: "Montserrat", sans-serif;
}

.software-description {
  color: var(--text-secondary);
  margin: 0 0 var(--spacing-md);
  line-height: 1.6;
  flex-grow: 1;
}

/* Learn More Button */
.learn-more-btn {
  align-self: flex-start;
  padding: 0.75rem 1.5rem;
  background: var(--primary-color);
  color: #fff;
  border: none;
  border-radius: 999px;
  font-size: 0.95rem;
  font-weight: 500;
  display: flex;
  align-items: center;
  gap: 0.5rem;
  cursor: pointer;
  transition: background 0.3s ease, transform 0.3s ease;
  text-transform: uppercase;
  letter-spacing: 0.05rem;
}

.learn-more-btn:hover {
  background: var(--secondary-color);
  transform: translateY(-2px) scale(1.02);
}

.btn-arrow {
  font-size: 1.1rem;
  transition: transform 0.3s ease;
}

.learn-more-btn:hover .btn-arrow {
  transform: translateX(4px);
}

/* Keyframes for Fade In Up Animation */
@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

/* Refined Contact Section */
.contact {
  padding: var(--spacing-lg) 0;
  background: var(--background-light);
}

.contact-inner {
  max-width: 800px;
  margin: 0 auto;
  padding: 0 var(--spacing-md);
}

.contact-content {
  background: white;
  padding: var(--spacing-lg);
  border-radius: var(--border-radius);
  box-shadow: 0 8px 32px rgba(0, 0, 0, 0.05);
}

.contact-title {
  font-size: 2.5rem;
  margin: 0 0 var(--spacing-xs);
  font-weight: 600;
  text-align: center;
}

.contact-subtitle {
  font-size: 1.25rem;
  color: var(--text-secondary);
  margin: 0 0 var(--spacing-lg);
  text-align: center;
}

.contact-form {
  display: flex;
  flex-direction: column;
  gap: var(--spacing-md);
}

.form-group {
  display: flex;
  flex-direction: column;
}

.contact-form input,
.contact-form textarea {
  padding: 1rem;
  border: 1px solid rgba(0, 0, 0, 0.1);
  border-radius: 0.75rem;
  font-size: 1rem;
  transition: all var(--transition-smooth);
  font-family: inherit;
}

.contact-form input:focus,
.contact-form textarea:focus {
  outline: none;
  border-color: var(--primary-color);
  box-shadow: 0 0 0 3px rgba(0, 102, 204, 0.1);
}

.contact-form textarea {
  min-height: 120px;
  resize: vertical;
}

/* Animations */
@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.fade-in-up {
  animation: fadeInUp 0.6s ease forwards;
  opacity: 0;
}

/* Responsive Design */
@media (max-width: 1024px) {
  .hero-title {
    font-size: 3rem;
  }
  
  .hero-subtitle {
    font-size: 1.25rem;
  }
  
  .section-title {
    font-size: 2rem;
  }
}

@media (max-width: 768px) {
  :root {
    --spacing-md: 1.5rem;
    --spacing-lg: 3rem;
  }

  .nav-inner {
    padding: var(--spacing-sm);
  }

  .nav-links {
    gap: var(--spacing-sm);
  }

  .hero {
    padding: calc(var(--spacing-lg) * 1.5) var(--spacing-sm);
  }

  .hero-title {
    font-size: 2.5rem;
  }

  .hero-subtitle {
    font-size: 1.125rem;
  }

  .hero-cta {
    flex-direction: column;
    gap: var(--spacing-sm);
  }

  .btn {
    width: 100%;
    justify-content: center;
  }

  .projects-grid,
  .services-grid,
  .software-grid {
    grid-template-columns: 1fr;
  }

  .contact-content {
    padding: var(--spacing-md);
  }

  .contact-title {
    font-size: 2rem;
  }
}

@media (max-width: 480px) {
  .hero-title {
    font-size: 2rem;
  }

  .section-title {
    font-size: 1.75rem;
  }

  .nav-link {
    font-size: 0.875rem;
  }
}

/* Accessibility Improvements */
@media (prefers-reduced-motion: reduce) {
  * {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
    scroll-behavior: auto !important;
  }
}

.visually-hidden {
  position: absolute;
  width: 1px;
  height: 1px;
  padding: 0;
  margin: -1px;
  overflow: hidden;
  clip: rect(0, 0, 0, 0);
  white-space: nowrap;
  border: 0;
}
</style>