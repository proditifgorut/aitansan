<script setup lang="ts">
import { ref } from 'vue'
import { Plus, Folder, Code, Database, Settings, User, LogOut, Sparkles } from 'lucide-vue-next'

const projects = ref([
  {
    id: 1,
    name: 'E-commerce App',
    description: 'Online store dengan payment gateway',
    status: 'In Progress',
    framework: 'React + Supabase',
    lastUpdate: '2 jam yang lalu',
    progress: 75
  },
  {
    id: 2,
    name: 'Landing Page',
    description: 'Company profile website',
    status: 'Completed',
    framework: 'Vue + Tailwind',
    lastUpdate: '1 hari yang lalu',
    progress: 100
  },
  {
    id: 3,
    name: 'Admin Dashboard',
    description: 'Analytics dan reporting dashboard',
    status: 'Planning',
    framework: 'Next.js + PostgreSQL',
    lastUpdate: '3 hari yang lalu',
    progress: 25
  }
])

const quickActions = [
  {
    title: 'Buat Aplikasi Baru',
    description: 'Mulai project dengan AI prompt',
    icon: Plus,
    color: 'bg-blue-600 hover:bg-blue-700'
  },
  {
    title: 'Import dari Figma',
    description: 'Convert desain jadi kode',
    icon: Code,
    color: 'bg-purple-600 hover:bg-purple-700'
  },
  {
    title: 'Template Library',
    description: 'Pilih dari 100+ template',
    icon: Folder,
    color: 'bg-green-600 hover:bg-green-700'
  },
  {
    title: 'Connect Database',
    description: 'Setup Supabase/Firebase',
    icon: Database,
    color: 'bg-orange-600 hover:bg-orange-700'
  }
]
</script>

<template>
  <div class="min-h-screen bg-gray-50 dark:bg-gray-900">
    <!-- Header -->
    <header class="bg-white dark:bg-gray-800 shadow-sm border-b border-gray-200 dark:border-gray-700">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="flex justify-between items-center h-16">
          <div class="flex items-center space-x-3">
            <Sparkles class="h-8 w-8 text-blue-600" />
            <h1 class="text-xl font-bold text-gray-900 dark:text-white">AI Unified Builder</h1>
          </div>
          
          <div class="flex items-center space-x-4">
            <button class="p-2 text-gray-400 hover:text-gray-600 dark:hover:text-gray-200">
              <Settings class="h-5 w-5" />
            </button>
            <button class="p-2 text-gray-400 hover:text-gray-600 dark:hover:text-gray-200">
              <User class="h-5 w-5" />
            </button>
            <button class="p-2 text-gray-400 hover:text-gray-600 dark:hover:text-gray-200">
              <LogOut class="h-5 w-5" />
            </button>
          </div>
        </div>
      </div>
    </header>

    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-8">
      <!-- Welcome Section -->
      <div class="mb-8">
        <h1 class="text-3xl font-bold text-gray-900 dark:text-white mb-2">
          Selamat datang kembali! 👋
        </h1>
        <p class="text-gray-600 dark:text-gray-300">
          Lanjutkan membangun aplikasi impian Anda dengan AI
        </p>
      </div>

      <!-- Quick Actions -->
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6 mb-8">
        <div 
          v-for="action in quickActions" 
          :key="action.title"
          :class="[
            'p-6 rounded-xl text-white cursor-pointer transition-all duration-300 hover:scale-105 shadow-lg',
            action.color
          ]"
        >
          <component :is="action.icon" class="h-8 w-8 mb-4" />
          <h3 class="font-semibold mb-2">{{ action.title }}</h3>
          <p class="text-sm opacity-90">{{ action.description }}</p>
        </div>
      </div>

      <!-- Recent Projects -->
      <div class="bg-white dark:bg-gray-800 rounded-xl shadow-lg p-6">
        <div class="flex justify-between items-center mb-6">
          <h2 class="text-xl font-bold text-gray-900 dark:text-white">Project Terbaru</h2>
          <button class="text-blue-600 hover:text-blue-700 font-medium">Lihat Semua</button>
        </div>
        
        <div class="space-y-4">
          <div 
            v-for="project in projects" 
            :key="project.id"
            class="p-4 border border-gray-200 dark:border-gray-700 rounded-lg hover:shadow-md transition-shadow cursor-pointer"
          >
            <div class="flex justify-between items-start mb-3">
              <div>
                <h3 class="font-semibold text-gray-900 dark:text-white mb-1">{{ project.name }}</h3>
                <p class="text-gray-600 dark:text-gray-300 text-sm">{{ project.description }}</p>
              </div>
              <span 
                :class="[
                  'px-2 py-1 rounded-full text-xs',
                  project.status === 'Completed' ? 'bg-green-100 text-green-800' :
                  project.status === 'In Progress' ? 'bg-blue-100 text-blue-800' :
                  'bg-yellow-100 text-yellow-800'
                ]"
              >
                {{ project.status }}
              </span>
            </div>
            
            <div class="flex justify-between items-center text-sm text-gray-500">
              <span>{{ project.framework }}</span>
              <span>{{ project.lastUpdate }}</span>
            </div>
            
            <div class="mt-3">
              <div class="flex justify-between text-sm text-gray-600 dark:text-gray-300 mb-1">
                <span>Progress</span>
                <span>{{ project.progress }}%</span>
              </div>
              <div class="w-full bg-gray-200 dark:bg-gray-700 rounded-full h-2">
                <div 
                  :class="[
                    'h-2 rounded-full transition-all duration-300',
                    project.progress === 100 ? 'bg-green-500' : 'bg-blue-500'
                  ]"
                  :style="{ width: `${project.progress}%` }"
                ></div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
