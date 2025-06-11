<template>
  <div class="min-h-screen gradient-bg">
    <NuxtRouteAnnouncer />
    
    <!-- Navigation -->
    <nav class="fixed top-0 w-full z-50 bg-gray-900/80 backdrop-blur-sm border-b border-gray-800">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="flex items-center justify-between h-16">
          <div class="flex-shrink-0">
            <NuxtLink to="/" class="text-xl font-bold gradient-text hover:opacity-80 transition-opacity duration-300">
              John.dev
            </NuxtLink>
          </div>
          <div class="hidden md:block">
            <div class="ml-10 flex items-baseline space-x-8">
              <a href="#home" class="hover:text-blue-400 transition-colors duration-300">Home</a>
              <a href="#about" class="hover:text-blue-400 transition-colors duration-300">About</a>
              <a href="#skills" class="hover:text-blue-400 transition-colors duration-300">Skills</a>
              <NuxtLink to="/projects" class="hover:text-blue-400 transition-colors duration-300">Projects</NuxtLink>
              <a href="#contact" class="hover:text-blue-400 transition-colors duration-300">Contact</a>
            </div>
          </div>
          <div class="md:hidden">
            <button @click="toggleMobileMenu" class="text-gray-300 hover:text-white">
              <Icon name="heroicons:bars-3" class="h-6 w-6" />
            </button>
          </div>
        </div>
      </div>
      
      <!-- Mobile menu -->
      <div v-show="mobileMenuOpen" class="md:hidden bg-gray-800 border-t border-gray-700">
        <div class="px-2 pt-2 pb-3 space-y-1">
          <a href="#home" @click="closeMobileMenu" class="block px-3 py-2 hover:text-blue-400 transition-colors duration-300">Home</a>
          <a href="#about" @click="closeMobileMenu" class="block px-3 py-2 hover:text-blue-400 transition-colors duration-300">About</a>
          <a href="#skills" @click="closeMobileMenu" class="block px-3 py-2 hover:text-blue-400 transition-colors duration-300">Skills</a>
          <NuxtLink to="/projects" @click="closeMobileMenu" class="block px-3 py-2 hover:text-blue-400 transition-colors duration-300">Projects</NuxtLink>
          <a href="#contact" @click="closeMobileMenu" class="block px-3 py-2 hover:text-blue-400 transition-colors duration-300">Contact</a>
        </div>
      </div>
    </nav>

    <!-- Hero Section -->
    <section id="home" class="min-h-screen flex items-center justify-center px-4 sm:px-6 lg:px-8">
      <div class="max-w-4xl mx-auto text-center">
        <div class="opacity-0 fade-in-up">
          <h1 class="text-4xl sm:text-6xl lg:text-7xl font-bold mb-6">
            Hi, I'm <span class="gradient-text">John</span>
          </h1>
          <p class="text-xl sm:text-2xl lg:text-3xl text-gray-300 mb-4 opacity-0 fade-in-up stagger-1">
            Software Engineer
          </p>
          <p class="text-lg sm:text-xl text-gray-400 mb-12 max-w-3xl mx-auto opacity-0 fade-in-up stagger-2">
            I build scalable web applications and cloud solutions using Python, Django, AWS, and GCP. 
            Passionate about creating efficient, maintainable code that solves real-world problems.
          </p>
          <div class="flex flex-col sm:flex-row gap-4 justify-center opacity-0 fade-in-up stagger-3">
            <a href="#contact" class="btn-primary">Get In Touch</a>
            <NuxtLink to="/projects" class="btn-secondary">View My Work</NuxtLink>
          </div>
        </div>
        
        <!-- Floating Elements -->
        <div class="absolute inset-0 pointer-events-none overflow-hidden">
          <div class="absolute top-1/4 left-10 float-animation">
            <div class="w-12 h-12 bg-blue-500/20 rounded-full blur-xl"></div>
          </div>
          <div class="absolute top-1/3 right-20 float-animation" style="animation-delay: 2s;">
            <div class="w-8 h-8 bg-purple-500/20 rounded-full blur-lg"></div>
          </div>
          <div class="absolute bottom-1/4 left-1/4 float-animation" style="animation-delay: 4s;">
            <div class="w-16 h-16 bg-emerald-500/20 rounded-full blur-2xl"></div>
          </div>
        </div>
      </div>
    </section>

    <!-- About Section -->
    <section id="about" class="py-20 px-4 sm:px-6 lg:px-8">
      <div class="max-w-6xl mx-auto">
        <div class="text-center mb-16">
          <h2 class="text-3xl sm:text-4xl font-bold mb-4 gradient-text">About Me</h2>
          <p class="text-xl text-gray-400 max-w-3xl mx-auto">
            Passionate software engineer with expertise in full-stack development and cloud architecture
          </p>
        </div>
        
        <div class="grid lg:grid-cols-2 gap-12 items-center">
          <div class="space-y-6">
            <p class="text-lg text-gray-300 leading-relaxed">
              With over 5 years of experience in software development, I specialize in building robust, 
              scalable applications using modern technologies. My expertise spans from backend development 
              with Python and Django to cloud infrastructure management on AWS and GCP.
            </p>
            <p class="text-lg text-gray-300 leading-relaxed">
              I'm passionate about writing clean, maintainable code and following best practices in 
              software architecture. I enjoy tackling complex problems and finding elegant solutions 
              that drive business value.
            </p>
            
            <div class="grid grid-cols-2 gap-6 mt-8">
              <div class="text-center p-4 bg-gray-800/50 rounded-lg card-hover">
                <h3 class="text-2xl font-bold text-blue-400 mb-2">5+</h3>
                <p class="text-gray-400">Years Experience</p>
              </div>
              <div class="text-center p-4 bg-gray-800/50 rounded-lg card-hover">
                <h3 class="text-2xl font-bold text-purple-400 mb-2">50+</h3>
                <p class="text-gray-400">Projects Completed</p>
              </div>
            </div>
          </div>
          
          <div class="relative">
            <div class="bg-gradient-to-br from-gray-800 to-gray-900 p-8 rounded-2xl shadow-2xl">
              <h3 class="text-xl font-semibold mb-6 text-center">Technical Focus</h3>
              <div class="space-y-4">
                <div class="flex items-center justify-between">
                  <span class="text-gray-300">Backend Development</span>
                  <div class="w-32 bg-gray-700 rounded-full h-2">
                    <div class="bg-blue-500 h-2 rounded-full w-5/6"></div>
                  </div>
                </div>
                <div class="flex items-center justify-between">
                  <span class="text-gray-300">Cloud Architecture</span>
                  <div class="w-32 bg-gray-700 rounded-full h-2">
                    <div class="bg-purple-500 h-2 rounded-full w-4/5"></div>
                  </div>
                </div>
                <div class="flex items-center justify-between">
                  <span class="text-gray-300">Database Design</span>
                  <div class="w-32 bg-gray-700 rounded-full h-2">
                    <div class="bg-emerald-500 h-2 rounded-full w-3/4"></div>
                  </div>
                </div>
                <div class="flex items-center justify-between">
                  <span class="text-gray-300">DevOps & CI/CD</span>
                  <div class="w-32 bg-gray-700 rounded-full h-2">
                    <div class="bg-orange-500 h-2 rounded-full w-4/5"></div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Skills Section -->
    <section id="skills" class="py-20 px-4 sm:px-6 lg:px-8 bg-gray-800/30">
      <div class="max-w-6xl mx-auto">
        <div class="text-center mb-16">
          <h2 class="text-3xl sm:text-4xl font-bold mb-4 gradient-text">Technical Skills</h2>
          <p class="text-xl text-gray-400 max-w-3xl mx-auto">
            Technologies and tools I use to build exceptional software solutions
          </p>
        </div>
        
        <div class="grid md:grid-cols-2 lg:grid-cols-4 gap-8">
          <!-- Python -->
          <div class="bg-gradient-to-br from-gray-800 to-gray-900 p-8 rounded-2xl text-center card-hover group">
            <div class="w-16 h-16 mx-auto mb-4 bg-yellow-500/20 rounded-full flex items-center justify-center group-hover:bg-yellow-500/30 transition-colors duration-300">
              <Icon name="logos:python" class="w-10 h-10" />
            </div>
            <h3 class="text-xl font-semibold mb-2">Python</h3>
            <p class="text-gray-400 text-sm">Backend development, automation, data processing</p>
          </div>
          
          <!-- Django -->
          <div class="bg-gradient-to-br from-gray-800 to-gray-900 p-8 rounded-2xl text-center card-hover group">
            <div class="w-16 h-16 mx-auto mb-4 bg-green-500/20 rounded-full flex items-center justify-center group-hover:bg-green-500/30 transition-colors duration-300">
              <Icon name="logos:django" class="w-10 h-10" />
            </div>
            <h3 class="text-xl font-semibold mb-2">Django</h3>
            <p class="text-gray-400 text-sm">Web framework, REST APIs, database modeling</p>
          </div>
          
          <!-- AWS -->
          <div class="bg-gradient-to-br from-gray-800 to-gray-900 p-8 rounded-2xl text-center card-hover group">
            <div class="w-16 h-16 mx-auto mb-4 bg-orange-500/20 rounded-full flex items-center justify-center group-hover:bg-orange-500/30 transition-colors duration-300">
              <Icon name="logos:aws" class="w-10 h-10" />
            </div>
            <h3 class="text-xl font-semibold mb-2">AWS</h3>
            <p class="text-gray-400 text-sm">EC2, S3, Lambda, RDS, CloudFormation</p>
          </div>
          
          <!-- GCP -->
          <div class="bg-gradient-to-br from-gray-800 to-gray-900 p-8 rounded-2xl text-center card-hover group">
            <div class="w-16 h-16 mx-auto mb-4 bg-blue-500/20 rounded-full flex items-center justify-center group-hover:bg-blue-500/30 transition-colors duration-300">
              <Icon name="logos:google-cloud" class="w-10 h-10" />
            </div>
            <h3 class="text-xl font-semibold mb-2">Google Cloud</h3>
            <p class="text-gray-400 text-sm">Compute Engine, Cloud Functions, BigQuery</p>
          </div>
        </div>
        
        <!-- Additional Skills -->
        <div class="mt-16">
          <h3 class="text-2xl font-semibold text-center mb-8">Other Technologies</h3>
          <div class="flex flex-wrap justify-center gap-4">
            <span class="px-4 py-2 bg-gray-800 rounded-full text-sm hover:bg-gray-700 transition-colors duration-300">PostgreSQL</span>
            <span class="px-4 py-2 bg-gray-800 rounded-full text-sm hover:bg-gray-700 transition-colors duration-300">Redis</span>
            <span class="px-4 py-2 bg-gray-800 rounded-full text-sm hover:bg-gray-700 transition-colors duration-300">Docker</span>
            <span class="px-4 py-2 bg-gray-800 rounded-full text-sm hover:bg-gray-700 transition-colors duration-300">Kubernetes</span>
            <span class="px-4 py-2 bg-gray-800 rounded-full text-sm hover:bg-gray-700 transition-colors duration-300">Git</span>
            <span class="px-4 py-2 bg-gray-800 rounded-full text-sm hover:bg-gray-700 transition-colors duration-300">Linux</span>
            <span class="px-4 py-2 bg-gray-800 rounded-full text-sm hover:bg-gray-700 transition-colors duration-300">Nginx</span>
            <span class="px-4 py-2 bg-gray-800 rounded-full text-sm hover:bg-gray-700 transition-colors duration-300">REST APIs</span>
            <span class="px-4 py-2 bg-gray-800 rounded-full text-sm hover:bg-gray-700 transition-colors duration-300">GraphQL</span>
            <span class="px-4 py-2 bg-gray-800 rounded-full text-sm hover:bg-gray-700 transition-colors duration-300">Terraform</span>
          </div>
        </div>
      </div>
    </section>

    <!-- Contact Section -->
    <section id="contact" class="py-20 px-4 sm:px-6 lg:px-8">
      <div class="max-w-4xl mx-auto">
        <div class="text-center mb-16">
          <h2 class="text-3xl sm:text-4xl font-bold mb-4 gradient-text">Get In Touch</h2>
          <p class="text-xl text-gray-400 max-w-2xl mx-auto">
            Let's discuss your next project or explore opportunities to work together
          </p>
        </div>
        
        <div class="grid md:grid-cols-2 gap-12">
          <!-- Contact Info -->
          <div class="space-y-8">
            <div class="flex items-center space-x-4 p-4 bg-gray-800/50 rounded-lg card-hover">
              <div class="w-12 h-12 bg-blue-500/20 rounded-full flex items-center justify-center">
                <Icon name="heroicons:envelope" class="w-6 h-6 text-blue-400" />
              </div>
              <div>
                <h3 class="font-semibold">Email</h3>
                <p class="text-gray-400">john@developer.com</p>
              </div>
            </div>
            
            <div class="flex items-center space-x-4 p-4 bg-gray-800/50 rounded-lg card-hover">
              <div class="w-12 h-12 bg-purple-500/20 rounded-full flex items-center justify-center">
                <Icon name="heroicons:phone" class="w-6 h-6 text-purple-400" />
              </div>
              <div>
                <h3 class="font-semibold">Phone</h3>
                <p class="text-gray-400">+1 (555) 123-4567</p>
              </div>
            </div>
            
            <div class="flex items-center space-x-4 p-4 bg-gray-800/50 rounded-lg card-hover">
              <div class="w-12 h-12 bg-emerald-500/20 rounded-full flex items-center justify-center">
                <Icon name="heroicons:map-pin" class="w-6 h-6 text-emerald-400" />
              </div>
              <div>
                <h3 class="font-semibold">Location</h3>
                <p class="text-gray-400">San Francisco, CA</p>
              </div>
            </div>
            
            <!-- Social Links -->
            <div class="pt-8">
              <h3 class="text-lg font-semibold mb-4">Connect With Me</h3>
              <div class="flex space-x-4">
                <a href="#" class="w-12 h-12 bg-gray-800 rounded-full flex items-center justify-center hover:bg-blue-600 transition-colors duration-300">
                  <Icon name="bi:linkedin" class="w-5 h-5" />
                </a>
                <a href="#" class="w-12 h-12 bg-gray-800 rounded-full flex items-center justify-center hover:bg-gray-700 transition-colors duration-300">
                  <Icon name="bi:github" class="w-5 h-5" />
                </a>
                <a href="#" class="w-12 h-12 bg-gray-800 rounded-full flex items-center justify-center hover:bg-blue-400 transition-colors duration-300">
                  <Icon name="bi:twitter" class="w-5 h-5" />
                </a>
              </div>
            </div>
          </div>
          
          <!-- Contact Form -->
          <div class="bg-gradient-to-br from-gray-800 to-gray-900 p-8 rounded-2xl">
            <form @submit.prevent="submitForm" class="space-y-6">
              <div>
                <label for="name" class="block text-sm font-medium text-gray-300 mb-2">Name</label>
                <input 
                  type="text" 
                  id="name" 
                  v-model="form.name"
                  class="w-full px-4 py-3 bg-gray-700 border border-gray-600 rounded-lg focus:outline-none focus:border-blue-500 focus:ring-2 focus:ring-blue-500/20 transition-colors duration-300"
                  required
                >
              </div>
              <div>
                <label for="email" class="block text-sm font-medium text-gray-300 mb-2">Email</label>
                <input 
                  type="email" 
                  id="email" 
                  v-model="form.email"
                  class="w-full px-4 py-3 bg-gray-700 border border-gray-600 rounded-lg focus:outline-none focus:border-blue-500 focus:ring-2 focus:ring-blue-500/20 transition-colors duration-300"
                  required
                >
              </div>
              <div>
                <label for="message" class="block text-sm font-medium text-gray-300 mb-2">Message</label>
                <textarea 
                  id="message" 
                  v-model="form.message"
                  rows="4" 
                  class="w-full px-4 py-3 bg-gray-700 border border-gray-600 rounded-lg focus:outline-none focus:border-blue-500 focus:ring-2 focus:ring-blue-500/20 transition-colors duration-300 resize-none"
                  required
                ></textarea>
              </div>
              <button type="submit" class="w-full btn-primary">
                Send Message
              </button>
            </form>
          </div>
        </div>
      </div>
    </section>

    <!-- Footer -->
    <footer class="py-8 px-4 sm:px-6 lg:px-8 border-t border-gray-800">
      <div class="max-w-6xl mx-auto text-center text-gray-400">
        <p>&copy; 2025 John Developer. All rights reserved.</p>
      </div>
    </footer>
  </div>
</template>

<script setup>
import { ref } from 'vue'

// Mobile menu state
const mobileMenuOpen = ref(false)

// Contact form state
const form = ref({
  name: '',
  email: '',
  message: ''
})

const toggleMobileMenu = () => {
  mobileMenuOpen.value = !mobileMenuOpen.value
}

const closeMobileMenu = () => {
  mobileMenuOpen.value = false
}

const submitForm = () => {
  // Handle form submission here
  console.log('Form submitted:', form.value)
  alert('Thank you for your message! I\'ll get back to you soon.')
  
  // Reset form
  form.value = {
    name: '',
    email: '',
    message: ''
  }
}

// Add scroll animations
onMounted(() => {
  const observerOptions = {
    threshold: 0.1,
    rootMargin: '0px 0px -50px 0px'
  }
  
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        entry.target.classList.add('fade-in-up')
      }
    })
  }, observerOptions)
  
  // Observe elements for animations
  document.querySelectorAll('section').forEach(section => {
    observer.observe(section)
  })
})
</script>