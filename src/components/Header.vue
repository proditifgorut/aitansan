<script setup lang="ts">
import { ref } from 'vue'
import { Menu, X, Sparkles, Sun, Moon } from 'lucide-vue-next'

const isMenuOpen = ref(false)
const isDark = ref(false)

const toggleTheme = () => {
  isDark.value = !isDark.value
  document.documentElement.classList.toggle('dark')
}
</script>

<template>
  <header class="fixed top-0 w-full bg-white/90 dark:bg-gray-900/90 backdrop-blur-md border-b border-gray-200 dark:border-gray-800 z-50">
    <nav class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="flex justify-between items-center h-16">
        <!-- Logo -->
        <div class="flex items-center space-x-2">
          <Sparkles class="h-8 w-8 text-blue-600" />
          <span class="text-xl font-bold gradient-text">AI Unified Builder</span>
        </div>

        <!-- Desktop Navigation -->
        <div class="hidden md:flex items-center space-x-8">
          <a href="#features" class="text-gray-700 dark:text-gray-300 hover:text-blue-600 transition-colors">Fitur</a>
          <a href="#demo" class="text-gray-700 dark:text-gray-300 hover:text-blue-600 transition-colors">Demo</a>
          <a href="#integrations" class="text-gray-700 dark:text-gray-300 hover:text-blue-600 transition-colors">Integrasi</a>
          <a href="#pricing" class="text-gray-700 dark:text-gray-300 hover:text-blue-600 transition-colors">Harga</a>
          <a href="#testimonials" class="text-gray-700 dark:text-gray-300 hover:text-blue-600 transition-colors">Testimoni</a>
          
          <!-- Theme Toggle -->
          <button @click="toggleTheme" class="p-2 rounded-lg hover:bg-gray-100 dark:hover:bg-gray-800 transition-colors">
            <Sun v-if="isDark" class="h-5 w-5 text-gray-600 dark:text-gray-300" />
            <Moon v-else class="h-5 w-5 text-gray-600 dark:text-gray-300" />
          </button>
          
          <button class="bg-blue-600 hover:bg-blue-700 text-white px-6 py-2 rounded-lg transition-colors">
            Mulai Gratis
          </button>
        </div>

        <!-- Mobile Menu Button -->
        <button 
          @click="isMenuOpen = !isMenuOpen"
          class="md:hidden p-2 rounded-md text-gray-700 dark:text-gray-300"
        >
          <Menu v-if="!isMenuOpen" class="h-6 w-6" />
          <X v-else class="h-6 w-6" />
        </button>
      </div>

      <!-- Mobile Navigation -->
      <div v-if="isMenuOpen" class="md:hidden py-4 border-t border-gray-200 dark:border-gray-800">
        <div class="flex flex-col space-y-4">
          <a href="#features" class="text-gray-700 dark:text-gray-300 hover:text-blue-600 transition-colors">Fitur</a>
          <a href="#demo" class="text-gray-700 dark:text-gray-300 hover:text-blue-600 transition-colors">Demo</a>
          <a href="#integrations" class="text-gray-700 dark:text-gray-300 hover:text-blue-600 transition-colors">Integrasi</a>
          <a href="#pricing" class="text-gray-700 dark:text-gray-300 hover:text-blue-600 transition-colors">Harga</a>
          <a href="#testimonials" class="text-gray-700 dark:text-gray-300 hover:text-blue-600 transition-colors">Testimoni</a>
          <button class="bg-blue-600 hover:bg-blue-700 text-white px-6 py-2 rounded-lg transition-colors w-full">
            Mulai Gratis
          </button>
        </div>
      </div>
    </nav>
  </header>
</template>
