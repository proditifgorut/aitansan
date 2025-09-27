<script setup lang="ts">
import { ref, onMounted } from 'vue'
import { Github, Database, Figma, Globe, Zap, Smartphone, Code, Cloud, Shield, Cpu } from 'lucide-vue-next'

const isVisible = ref(false)

const integrations = [
  {
    icon: Figma,
    name: 'Figma',
    description: 'Desain ke React/Flutter',
    color: 'bg-purple-100 text-purple-600 dark:bg-purple-900/20',
    category: 'Design'
  },
  {
    icon: Github,
    name: 'GitHub',
    description: 'Sinkronisasi kode',
    color: 'bg-gray-100 text-gray-600 dark:bg-gray-800',
    category: 'Version Control'
  },
  {
    icon: Database,
    name: 'Supabase',
    description: 'Database, Auth, Storage',
    color: 'bg-green-100 text-green-600 dark:bg-green-900/20',
    category: 'Backend'
  },
  {
    icon: Globe,
    name: 'Vercel',
    description: 'Deploy instan',
    color: 'bg-black text-white',
    category: 'Deployment'
  },
  {
    icon: Zap,
    name: 'Netlify',
    description: 'Hosting static site',
    color: 'bg-teal-100 text-teal-600 dark:bg-teal-900/20',
    category: 'Deployment'
  },
  {
    icon: Smartphone,
    name: 'Flutter',
    description: 'Export aplikasi mobile',
    color: 'bg-blue-100 text-blue-600 dark:bg-blue-900/20',
    category: 'Mobile'
  },
  {
    icon: Code,
    name: 'VS Code',
    description: 'Extension editor',
    color: 'bg-blue-100 text-blue-700 dark:bg-blue-900/20',
    category: 'Development'
  },
  {
    icon: Cloud,
    name: 'AWS',
    description: 'Cloud deployment',
    color: 'bg-orange-100 text-orange-600 dark:bg-orange-900/20',
    category: 'Cloud'
  },
  {
    icon: Shield,
    name: 'Auth0',
    description: 'Authentication',
    color: 'bg-indigo-100 text-indigo-600 dark:bg-indigo-900/20',
    category: 'Security'
  },
  {
    icon: Cpu,
    name: 'OpenAI',
    description: 'AI processing',
    color: 'bg-green-100 text-green-700 dark:bg-green-900/20',
    category: 'AI'
  }
]

const workflowSteps = [
  { name: 'Desain', icon: Figma, color: 'text-purple-600' },
  { name: 'AI Build', icon: Zap, color: 'text-blue-600' },
  { name: 'Git Sync', icon: Github, color: 'text-gray-600' },
  { name: 'Deploy', icon: Globe, color: 'text-green-600' }
]

onMounted(() => {
  const observer = new IntersectionObserver((entries) => {
    entries.forEach((entry) => {
      if (entry.isIntersecting) {
        isVisible.value = true
      }
    })
  })
  
  const element = document.getElementById('integrations')
  if (element) {
    observer.observe(element)
  }
})
</script>

<template>
  <section id="integrations" class="py-20 bg-white dark:bg-gray-900">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="text-center mb-16">
        <h2 class="text-4xl md:text-5xl font-bold mb-4">
          <span class="gradient-text">Integrasi Yang Mulus</span>
        </h2>
        <p class="text-xl text-gray-600 dark:text-gray-300 max-w-3xl mx-auto">
          Terhubung dengan tools dan platform favorit Anda untuk workflow pengembangan yang lengkap
        </p>
      </div>

      <!-- Integration Grid -->
      <div class="grid grid-cols-2 md:grid-cols-3 lg:grid-cols-5 gap-6 mb-16">
        <div 
          v-for="(integration, index) in integrations" 
          :key="integration.name"
          :class="[
            'feature-card text-center group transition-all duration-700',
            isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10'
          ]"
          :style="{ transitionDelay: `${index * 100}ms` }"
        >
          <div :class="['p-4 rounded-xl mb-4 mx-auto w-fit group-hover:scale-110 transition-transform', integration.color]">
            <component :is="integration.icon" class="h-8 w-8" />
          </div>
          <h3 class="text-lg font-semibold mb-2 text-gray-900 dark:text-white">
            {{ integration.name }}
          </h3>
          <p class="text-sm text-gray-600 dark:text-gray-300 mb-2">
            {{ integration.description }}
          </p>
          <span class="text-xs px-2 py-1 bg-gray-100 dark:bg-gray-800 rounded-full text-gray-500">
            {{ integration.category }}
          </span>
        </div>
      </div>

      <!-- Workflow -->
      <div class="bg-gradient-to-r from-blue-50 to-purple-50 dark:from-gray-800 dark:to-gray-900 rounded-2xl p-8 mb-16">
        <h3 class="text-2xl font-bold text-center mb-8 text-gray-900 dark:text-white">
          Workflow Pengembangan Modern
        </h3>
        <div class="flex flex-col md:flex-row items-center justify-center space-y-4 md:space-y-0 md:space-x-8">
          <div v-for="(step, index) in workflowSteps" :key="step.name" class="flex items-center">
            <div class="flex items-center space-x-2 bg-white dark:bg-gray-800 px-6 py-3 rounded-xl shadow-lg">
              <component :is="step.icon" :class="['h-6 w-6', step.color]" />
              <span class="font-medium text-gray-900 dark:text-white">{{ step.name }}</span>
            </div>
            <div v-if="index < workflowSteps.length - 1" class="hidden md:block text-gray-400 mx-4">
              →
            </div>
          </div>
        </div>
      </div>

      <!-- API Documentation -->
      <div class="grid grid-cols-1 md:grid-cols-2 gap-8">
        <div class="feature-card">
          <h4 class="text-xl font-semibold mb-4 text-gray-900 dark:text-white">API & SDK</h4>
          <ul class="space-y-2 text-gray-600 dark:text-gray-300">
            <li>• REST API lengkap dengan dokumentasi</li>
            <li>• SDK untuk JavaScript, Python, Go</li>
            <li>• Webhook untuk real-time updates</li>
            <li>• GraphQL support untuk query fleksibel</li>
          </ul>
        </div>
        <div class="feature-card">
          <h4 class="text-xl font-semibold mb-4 text-gray-900 dark:text-white">Enterprise Features</h4>
          <ul class="space-y-2 text-gray-600 dark:text-gray-300">
            <li>• SSO dengan SAML/OAuth</li>
            <li>• Audit logs dan compliance</li>
            <li>• Custom domains dan branding</li>
            <li>• Priority support dan SLA</li>
          </ul>
        </div>
      </div>
    </div>
  </section>
</template>
