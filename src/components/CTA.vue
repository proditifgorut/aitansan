<script setup lang="ts">
import { ArrowRight, Sparkles, Gift, Clock, Users } from 'lucide-vue-next'

const benefits = [
  {
    icon: Gift,
    text: 'Free trial 14 hari tanpa kartu kredit'
  },
  {
    icon: Clock,
    text: 'Setup dalam hitungan menit'
  },
  {
    icon: Users,
    text: 'Support 24/7 dalam bahasa Indonesia'
  }
]
</script>

<template>
  <section class="py-20 gradient-bg">
    <div class="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8 text-center">
      <div class="bg-white/80 dark:bg-gray-800/80 backdrop-blur-sm rounded-3xl p-12 shadow-2xl border border-gray-200/50 dark:border-gray-700/50">
        <Sparkles class="h-16 w-16 text-blue-600 mx-auto mb-6 animate-pulse" />
        
        <h2 class="text-4xl md:text-5xl font-bold mb-6">
          <span class="gradient-text">Siap Membangun Masa Depan?</span>
        </h2>
        
        <p class="text-xl text-gray-600 dark:text-gray-300 mb-8 max-w-2xl mx-auto">
          🚀 Dari ide menjadi aplikasi hanya dalam hitungan menit. Mulai membangun dengan AI Unified Builder dan 
          rasakan masa depan pengembangan aplikasi hari ini.
        </p>

        <!-- Benefits -->
        <div class="grid grid-cols-1 md:grid-cols-3 gap-6 mb-8">
          <div v-for="benefit in benefits" :key="benefit.text" class="flex items-center justify-center space-x-2 text-gray-700 dark:text-gray-300">
            <component :is="benefit.icon" class="h-5 w-5 text-green-500" />
            <span class="text-sm font-medium">{{ benefit.text }}</span>
          </div>
        </div>
        
        <div class="flex flex-col sm:flex-row gap-4 justify-center items-center mb-6">
          <button class="bg-blue-600 hover:bg-blue-700 text-white px-10 py-4 rounded-xl text-lg font-semibold transition-all duration-300 flex items-center space-x-2 hover:scale-105 shadow-lg">
            <span>Mulai Membangun Sekarang</span>
            <ArrowRight class="h-5 w-5" />
          </button>
          <button class="border-2 border-gray-300 dark:border-gray-600 text-gray-700 dark:text-gray-300 hover:border-blue-600 hover:text-blue-600 px-10 py-4 rounded-xl text-lg font-semibold transition-all duration-300 hover:scale-105">
            Jadwalkan Demo
          </button>
        </div>
        
        <p class="text-sm text-gray-500 dark:text-gray-400 mb-4">
          Tanpa kartu kredit • Tier gratis tersedia • Batal kapan saja
        </p>

        <!-- Money Back Guarantee -->
        <div class="inline-flex items-center space-x-2 bg-green-50 dark:bg-green-900/20 text-green-700 dark:text-green-300 px-4 py-2 rounded-full text-sm">
          <span>💯</span>
          <span class="font-medium">30 hari garansi uang kembali</span>
        </div>
      </div>
    </div>
  </section>
</template>
