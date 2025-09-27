<script setup lang="ts">
import { ref, onMounted } from 'vue'
import { Star, Quote } from 'lucide-vue-next'

const isVisible = ref(false)

const testimonials = [
  {
    name: 'Andi Prasetyo',
    role: 'Founder & CEO',
    company: 'TechStart Indonesia',
    avatar: 'https://img-wrapper.vercel.app/image?url=https://placehold.co/80x80.png',
    rating: 5,
    text: 'AI Unified Builder benar-benar mengubah cara kami mengembangkan produk. Dari ide ke MVP hanya butuh 2 hari, padahal biasanya 2 minggu. Tim kami bisa fokus ke bisnis logic daripada setup infrastruktur.'
  },
  {
    name: 'Sarah Wijaya',
    role: 'Lead Developer',
    company: 'Digital Agency Pro',
    avatar: 'https://img-wrapper.vercel.app/image?url=https://placehold.co/80x80.png',
    rating: 5,
    text: 'Kualitas kode yang dihasilkan sangat bersih dan mengikuti best practices. Klien kami sangat senang dengan kecepatan delivery project. Productivity tim meningkat 300%.'
  },
  {
    name: 'Budi Santoso',
    role: 'CTO',
    company: 'E-commerce Nusantara',
    avatar: 'https://img-wrapper.vercel.app/image?url=https://placehold.co/80x80.png',
    rating: 5,
    text: 'Fitur design-to-code nya luar biasa! Designer kami upload mockup Figma, langsung jadi komponen React yang responsive. Collaboration antara design dan development jadi seamless.'
  },
  {
    name: 'Maya Sari',
    role: 'Product Manager',
    company: 'Fintech Innovation',
    avatar: 'https://img-wrapper.vercel.app/image?url=https://placehold.co/80x80.png',
    rating: 5,
    text: 'Enterprise features seperti SSO dan audit logs sangat membantu compliance requirements kami. Support team juga sangat responsif dan knowledgeable.'
  },
  {
    name: 'Reza Firmansyah',
    role: 'Freelance Developer',
    company: 'Independent',
    avatar: 'https://img-wrapper.vercel.app/image?url=https://placehold.co/80x80.png',
    rating: 5,
    text: 'Sebagai freelancer, AI Unified Builder membantu saya mengerjakan project lebih banyak dengan quality yang konsisten. ROI nya sangat tinggi, langsung balik modal dalam sebulan.'
  },
  {
    name: 'Lisa Anggraeni',
    role: 'Startup Founder',
    company: 'EduTech Solutions',
    avatar: 'https://img-wrapper.vercel.app/image?url=https://placehold.co/80x80.png',
    rating: 5,
    text: 'Template yang disediakan sangat lengkap dan modern. Kami bisa launch platform edukasi online hanya dalam 1 minggu. User experience nya juga excellent di semua device.'
  }
]

const stats = [
  { value: '50K+', label: 'Developer Aktif' },
  { value: '99.8%', label: 'Customer Satisfaction' },
  { value: '10x', label: 'Faster Development' },
  { value: '24/7', label: 'Global Support' }
]

onMounted(() => {
  const observer = new IntersectionObserver((entries) => {
    entries.forEach((entry) => {
      if (entry.isIntersecting) {
        isVisible.value = true
      }
    })
  })
  
  const element = document.getElementById('testimonials')
  if (element) {
    observer.observe(element)
  }
})
</script>

<template>
  <section id="testimonials" class="py-20 bg-white dark:bg-gray-900">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="text-center mb-16">
        <h2 class="text-4xl md:text-5xl font-bold mb-4">
          <span class="gradient-text">Dipercaya Developer Indonesia</span>
        </h2>
        <p class="text-xl text-gray-600 dark:text-gray-300 max-w-3xl mx-auto">
          Ribuan developer dan perusahaan telah mempercayai AI Unified Builder untuk project mereka
        </p>
      </div>

      <!-- Stats -->
      <div class="grid grid-cols-2 md:grid-cols-4 gap-8 mb-16">
        <div 
          v-for="(stat, index) in stats" 
          :key="stat.label"
          :class="[
            'text-center transition-all duration-700',
            isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10'
          ]"
          :style="{ transitionDelay: `${index * 100}ms` }"
        >
          <div class="text-4xl font-bold text-blue-600 mb-2">{{ stat.value }}</div>
          <div class="text-gray-600 dark:text-gray-400">{{ stat.label }}</div>
        </div>
      </div>

      <!-- Testimonials Grid -->
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
        <div 
          v-for="(testimonial, index) in testimonials" 
          :key="testimonial.name"
          :class="[
            'feature-card transition-all duration-700',
            isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10'
          ]"
          :style="{ transitionDelay: `${index * 150}ms` }"
        >
          <div class="flex items-start space-x-4 mb-4">
            <img 
              :src="testimonial.avatar" 
              :alt="testimonial.name"
              class="w-12 h-12 rounded-full object-cover"
            />
            <div class="flex-1">
              <h4 class="font-semibold text-gray-900 dark:text-white">{{ testimonial.name }}</h4>
              <p class="text-sm text-gray-600 dark:text-gray-300">{{ testimonial.role }}</p>
              <p class="text-sm text-blue-600">{{ testimonial.company }}</p>
            </div>
            <Quote class="h-8 w-8 text-gray-300 dark:text-gray-600" />
          </div>

          <!-- Rating -->
          <div class="flex items-center space-x-1 mb-4">
            <div v-for="i in testimonial.rating" :key="i" class="text-yellow-400">
              <Star class="h-4 w-4 fill-current" />
            </div>
          </div>

          <!-- Testimonial Text -->
          <p class="text-gray-700 dark:text-gray-300 leading-relaxed">
            "{{ testimonial.text }}"
          </p>
        </div>
      </div>

      <!-- Trust Badges -->
      <div class="mt-16 text-center">
        <p class="text-gray-500 dark:text-gray-400 mb-8">Dipercaya oleh perusahaan terkemuka</p>
        <div class="flex flex-wrap justify-center items-center gap-8 opacity-60">
          <div class="bg-gray-100 dark:bg-gray-800 px-6 py-3 rounded-lg">
            <span class="font-semibold text-gray-700 dark:text-gray-300">Tokopedia</span>
          </div>
          <div class="bg-gray-100 dark:bg-gray-800 px-6 py-3 rounded-lg">
            <span class="font-semibold text-gray-700 dark:text-gray-300">Gojek</span>
          </div>
          <div class="bg-gray-100 dark:bg-gray-800 px-6 py-3 rounded-lg">
            <span class="font-semibold text-gray-700 dark:text-gray-300">Bukalapak</span>
          </div>
          <div class="bg-gray-100 dark:bg-gray-800 px-6 py-3 rounded-lg">
            <span class="font-semibold text-gray-700 dark:text-gray-300">Traveloka</span>
          </div>
          <div class="bg-gray-100 dark:bg-gray-800 px-6 py-3 rounded-lg">
            <span class="font-semibold text-gray-700 dark:text-gray-300">Blibli</span>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
