<template>
  <div class="min-h-screen gradient-bg">
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
              <NuxtLink to="/" class="hover:text-blue-400 transition-colors duration-300">Home</NuxtLink>
              <NuxtLink to="/#about" class="hover:text-blue-400 transition-colors duration-300">About</NuxtLink>
              <NuxtLink to="/#skills" class="hover:text-blue-400 transition-colors duration-300">Skills</NuxtLink>
              <NuxtLink to="/projects" class="text-blue-400 font-medium">Projects</NuxtLink>
              <NuxtLink to="/#contact" class="hover:text-blue-400 transition-colors duration-300">Contact</NuxtLink>
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
          <NuxtLink to="/" @click="closeMobileMenu" class="block px-3 py-2 hover:text-blue-400 transition-colors duration-300">Home</NuxtLink>
          <NuxtLink to="/#about" @click="closeMobileMenu" class="block px-3 py-2 hover:text-blue-400 transition-colors duration-300">About</NuxtLink>
          <NuxtLink to="/#skills" @click="closeMobileMenu" class="block px-3 py-2 hover:text-blue-400 transition-colors duration-300">Skills</NuxtLink>
          <NuxtLink to="/projects" @click="closeMobileMenu" class="block px-3 py-2 text-blue-400 font-medium">Projects</NuxtLink>
          <NuxtLink to="/#contact" @click="closeMobileMenu" class="block px-3 py-2 hover:text-blue-400 transition-colors duration-300">Contact</NuxtLink>
        </div>
      </div>
    </nav>

    <!-- Hero Section -->
    <section class="pt-24 pb-12 px-4 sm:px-6 lg:px-8">
      <div class="max-w-6xl mx-auto text-center">
        <h1 class="text-4xl sm:text-5xl lg:text-6xl font-bold mb-6 gradient-text">
          My Projects
        </h1>
        <p class="text-xl text-gray-400 max-w-3xl mx-auto mb-12">
          A showcase of my work in software engineering, featuring web applications, 
          cloud solutions, and automation tools built with Python, Django, AWS, and GCP.
        </p>
        
        <!-- Filter Buttons -->
        <div class="flex flex-wrap justify-center gap-4 mb-16">
          <button 
            @click="filterProjects('all')"
            :class="['px-6 py-2 rounded-full transition-all duration-300', 
                     activeFilter === 'all' ? 'bg-blue-500 text-white' : 'bg-gray-800 text-gray-300 hover:bg-gray-700']"
          >
            All Projects
          </button>
          <button 
            @click="filterProjects('web')"
            :class="['px-6 py-2 rounded-full transition-all duration-300', 
                     activeFilter === 'web' ? 'bg-blue-500 text-white' : 'bg-gray-800 text-gray-300 hover:bg-gray-700']"
          >
            Web Apps
          </button>
          <button 
            @click="filterProjects('cloud')"
            :class="['px-6 py-2 rounded-full transition-all duration-300', 
                     activeFilter === 'cloud' ? 'bg-blue-500 text-white' : 'bg-gray-800 text-gray-300 hover:bg-gray-700']"
          >
            Cloud Solutions
          </button>
          <button 
            @click="filterProjects('automation')"
            :class="['px-6 py-2 rounded-full transition-all duration-300', 
                     activeFilter === 'automation' ? 'bg-blue-500 text-white' : 'bg-gray-800 text-gray-300 hover:bg-gray-700']"
          >
            Automation
          </button>
        </div>
      </div>
    </section>

    <!-- Projects Grid -->
    <section class="pb-20 px-4 sm:px-6 lg:px-8">
      <div class="max-w-6xl mx-auto">
        <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-8">
          <div 
            v-for="project in filteredProjects" 
            :key="project.id"
            class="bg-gradient-to-br from-gray-800 to-gray-900 rounded-2xl overflow-hidden shadow-2xl card-hover group"
          >
            <!-- Project Image -->
            <div class="relative h-48 bg-gradient-to-br from-blue-500/20 to-purple-500/20 overflow-hidden">
              <div class="absolute inset-0 bg-gradient-to-br from-blue-500/10 to-purple-500/10 group-hover:from-blue-500/20 group-hover:to-purple-500/20 transition-all duration-300"></div>
              <div class="absolute inset-0 flex items-center justify-center">
                <Icon :name="project.icon" class="w-16 h-16 text-white/80" />
              </div>
              <!-- Status Badge -->
              <div class="absolute top-4 right-4">
                <span :class="['px-3 py-1 rounded-full text-xs font-medium', 
                               project.status === 'Live' ? 'bg-green-500/20 text-green-400 border border-green-500/30' : 
                               project.status === 'In Progress' ? 'bg-yellow-500/20 text-yellow-400 border border-yellow-500/30' :
                               'bg-blue-500/20 text-blue-400 border border-blue-500/30']">
                  {{ project.status }}
                </span>
              </div>
            </div>
            
            <!-- Project Content -->
            <div class="p-6">
              <div class="flex items-center justify-between mb-3">
                <h3 class="text-xl font-semibold text-white group-hover:text-blue-400 transition-colors duration-300">
                  {{ project.title }}
                </h3>
                <span class="text-sm text-gray-400">{{ project.year }}</span>
              </div>
              
              <p class="text-gray-400 text-sm mb-4 leading-relaxed">
                {{ project.description }}
              </p>
              
              <!-- Tech Stack -->
              <div class="flex flex-wrap gap-2 mb-6">
                <span 
                  v-for="tech in project.technologies" 
                  :key="tech"
                  class="px-2 py-1 bg-gray-700/50 rounded text-xs text-gray-300"
                >
                  {{ tech }}
                </span>
              </div>
              
              <!-- Project Links -->
              <div class="flex gap-3">
                <a 
                  v-if="project.liveUrl"
                  :href="project.liveUrl" 
                  target="_blank"
                  class="flex-1 bg-blue-500 hover:bg-blue-600 text-white text-center py-2 px-4 rounded-lg transition-colors duration-300 text-sm font-medium"
                >
                  <Icon name="heroicons:arrow-top-right-on-square" class="w-4 h-4 inline mr-1" />
                  Live Demo
                </a>
                <a 
                  v-if="project.githubUrl"
                  :href="project.githubUrl" 
                  target="_blank"
                  class="flex-1 bg-gray-700 hover:bg-gray-600 text-white text-center py-2 px-4 rounded-lg transition-colors duration-300 text-sm font-medium"
                >
                  <Icon name="bi:github" class="w-4 h-4 inline mr-1" />
                  Code
                </a>
              </div>
            </div>
          </div>
        </div>
        
        <!-- Empty State -->
        <div v-if="filteredProjects.length === 0" class="text-center py-16">
          <Icon name="heroicons:folder-open" class="w-16 h-16 text-gray-600 mx-auto mb-4" />
          <h3 class="text-xl font-semibold text-gray-400 mb-2">No projects found</h3>
          <p class="text-gray-500">Try selecting a different filter to see more projects.</p>
        </div>
      </div>
    </section>

    <!-- CTA Section -->
    <section class="py-20 px-4 sm:px-6 lg:px-8 bg-gray-800/30">
      <div class="max-w-4xl mx-auto text-center">
        <h2 class="text-3xl sm:text-4xl font-bold mb-6 gradient-text">
          Interested in Working Together?
        </h2>
        <p class="text-xl text-gray-400 mb-8 max-w-2xl mx-auto">
          I'm always open to discussing new opportunities and exciting projects. 
          Let's build something amazing together.
        </p>
        <div class="flex flex-col sm:flex-row gap-4 justify-center">
          <NuxtLink to="/#contact" class="btn-primary">
            Get In Touch
          </NuxtLink>
          <NuxtLink to="/" class="btn-secondary">
            Back to Home
          </NuxtLink>
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
import { ref, computed } from 'vue'

// SEO
useHead({
  title: 'Projects - John Developer',
  meta: [
    { name: 'description', content: 'Explore my portfolio of software engineering projects including web applications, cloud solutions, and automation tools built with Python, Django, AWS, and GCP.' }
  ]
})

// Mobile menu state
const mobileMenuOpen = ref(false)
const activeFilter = ref('all')

// Projects data
const projects = ref([
  {
    id: 1,
    title: 'E-Commerce Platform',
    description: 'A full-stack e-commerce solution built with Django and React, featuring payment integration, inventory management, and real-time analytics.',
    technologies: ['Python', 'Django', 'PostgreSQL', 'Redis', 'AWS S3', 'Stripe'],
    category: 'web',
    status: 'Live',
    year: '2024',
    icon: 'heroicons:shopping-cart',
    liveUrl: 'https://example.com',
    githubUrl: 'https://github.com'
  },
  {
    id: 2,
    title: 'Cloud Infrastructure Automation',
    description: 'Terraform-based infrastructure as code solution for AWS, automating deployment of scalable web applications with CI/CD pipelines.',
    technologies: ['Terraform', 'AWS', 'Docker', 'GitHub Actions', 'CloudFormation'],
    category: 'cloud',
    status: 'Live',
    year: '2024',
    icon: 'heroicons:cloud',
    githubUrl: 'https://github.com'
  },
  {
    id: 3,
    title: 'Data Processing Pipeline',
    description: 'Serverless data processing pipeline using AWS Lambda and GCP Cloud Functions to handle large-scale data transformation and analysis.',
    technologies: ['Python', 'AWS Lambda', 'GCP Cloud Functions', 'BigQuery', 'Apache Airflow'],
    category: 'automation',
    status: 'Live',
    year: '2023',
    icon: 'heroicons:cpu-chip',
    githubUrl: 'https://github.com'
  },
  {
    id: 4,
    title: 'Task Management API',
    description: 'RESTful API built with Django REST Framework, featuring JWT authentication, real-time notifications, and comprehensive task management.',
    technologies: ['Django', 'DRF', 'PostgreSQL', 'Celery', 'WebSockets', 'JWT'],
    category: 'web',
    status: 'Live',
    year: '2023',
    icon: 'heroicons:list-bullet',
    liveUrl: 'https://example.com',
    githubUrl: 'https://github.com'
  },
  {
    id: 5,
    title: 'Monitoring Dashboard',
    description: 'Real-time monitoring dashboard for cloud infrastructure using Grafana, Prometheus, and custom Python scripts for data collection.',
    technologies: ['Python', 'Grafana', 'Prometheus', 'Docker', 'AWS CloudWatch'],
    category: 'automation',
    status: 'Live',
    year: '2023',
    icon: 'heroicons:chart-bar',
    liveUrl: 'https://example.com'
  },
  {
    id: 6,
    title: 'Microservices Architecture',
    description: 'Scalable microservices architecture deployed on Kubernetes, featuring service mesh, API gateway, and distributed tracing.',
    technologies: ['Python', 'FastAPI', 'Kubernetes', 'Istio', 'PostgreSQL', 'Redis'],
    category: 'cloud',
    status: 'In Progress',
    year: '2024',
    icon: 'heroicons:squares-2x2',
    githubUrl: 'https://github.com'
  }
])

// Computed property for filtered projects
const filteredProjects = computed(() => {
  if (activeFilter.value === 'all') {
    return projects.value
  }
  return projects.value.filter(project => project.category === activeFilter.value)
})

const toggleMobileMenu = () => {
  mobileMenuOpen.value = !mobileMenuOpen.value
}

const closeMobileMenu = () => {
  mobileMenuOpen.value = false
}

const filterProjects = (category) => {
  activeFilter.value = category
}
</script>