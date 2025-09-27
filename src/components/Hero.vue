<script setup lang="ts">
import { ref, onMounted } from 'vue'
import { Zap, ArrowRight, Play, CheckCircle } from 'lucide-vue-next'

const isVisible = ref(false)

const benefits = [
  'Tanpa coding yang rumit',
  'Deploy dalam hitungan menit',
  'Gratis untuk memulai'
]

onMounted(() => {
  setTimeout(() => {
    isVisible.value = true
  }, 100)
})
</script>

<template>
  <section class="relative pt-32 pb-20 overflow-hidden gradient-bg">
    <!-- Background Elements -->
    <div class="absolute inset-0 overflow-hidden">
      <div class="absolute -top-40 -right-40 w-80 h-80 bg-blue-400/20 rounded-full blur-3xl animate-pulse-slow"></div>
      <div class="absolute -bottom-40 -left-40 w-80 h-80 bg-purple-400/20 rounded-full blur-3xl animate-pulse-slow" style="animation-delay: 2s;"></div>
    </div>

    <div class="relative max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 text-center">
      <!-- Main Heading -->
      <div 
        :class="['transition-all duration-1000', isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10']"
      >
        <h1 class="text-4xl md:text-6xl lg:text-7xl font-bold mb-6">
          <span class="gradient-text">✨ AI Unified Builder</span>
          <br>
          <span class="text-gray-900 dark:text-white">Dari Desain ke Aplikasi Full-Stack</span>
        </h1>
      </div>

      <!-- Description -->
      <div 
        :class="['transition-all duration-1000 delay-300', isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10']"
      >
        <p class="text-xl md:text-2xl text-gray-600 dark:text-gray-300 mb-8 max-w-4xl mx-auto leading-relaxed">
          Platform bertenaga AI yang memungkinkan Anda membangun aplikasi web dan mobile hanya dengan prompt teks alami atau desain visual, 
          lengkap dengan frontend modern, backend terintegrasi, dan sinkronisasi GitHub.
        </p>
      </div>

      <!-- Benefits -->
      <div 
        :class="['transition-all duration-1000 delay-400', isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10']"
      >
        <div class="flex flex-wrap justify-center items-center gap-6 mb-8">
          <div v-for="benefit in benefits" :key="benefit" class="flex items-center space-x-2 text-gray-700 dark:text-gray-300">
            <CheckCircle class="h-5 w-5 text-green-500" />
            <span class="font-medium">{{ benefit }}</span>
          </div>
        </div>
      </div>

      <!-- CTA Buttons -->
      <div 
        :class="['transition-all duration-1000 delay-500', isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10']"
      >
        <div class="flex flex-col sm:flex-row gap-4 justify-center items-center mb-12">
          <button class="bg-blue-600 hover:bg-blue-700 text-white px-8 py-4 rounded-xl text-lg font-semibold transition-all duration-300 flex items-center space-x-2 hover:scale-105 shadow-lg">
            <Zap class="h-5 w-5" />
            <span>🚀 Mulai Membangun Sekarang</span>
            <ArrowRight class="h-5 w-5" />
          </button>
          <button class="border-2 border-gray-300 dark:border-gray-600 text-gray-700 dark:text-gray-300 hover:border-blue-600 hover:text-blue-600 px-8 py-4 rounded-xl text-lg font-semibold transition-all duration-300 flex items-center space-x-2 hover:scale-105">
            <Play class="h-5 w-5" />
            <span>Tonton Demo</span>
          </button>
        </div>
      </div>

      <!-- Stats -->
      <div 
        :class="['transition-all duration-1000 delay-700', isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10']"
      >
        <div class="grid grid-cols-2 md:grid-cols-4 gap-8 max-w-3xl mx-auto">
          <div class="text-center">
            <div class="text-3xl font-bold text-blue-600">10rb+</div>
            <div class="text-gray-600 dark:text-gray-400">Aplikasi Dibuat</div>
          </div>
          <div class="text-center">
            <div class="text-3xl font-bold text-purple-600">99,9%</div>
            <div class="text-gray-600 dark:text-gray-400">Uptime</div>
          </div>
          <div class="text-center">
            <div class="text-3xl font-bold text-indigo-600">5 Menit</div>
            <div class="text-gray-600 dark:text-gray-400">Rata-rata Build</div>
          </div>
          <div class="text-center">
            <div class="text-3xl font-bold text-green-600">24/7</div>
            <div class="text-gray-600 dark:text-gray-400">Dukungan</div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
