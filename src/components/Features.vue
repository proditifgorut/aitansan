<script setup lang="ts">
import { ref, onMounted } from 'vue'
import { 
  MessageSquare, 
  Palette, 
  Brain, 
  Database, 
  Eye, 
  Layout,
  Users,
  Rocket,
  Shield,
  Zap,
  Code,
  Globe
} from 'lucide-vue-next'

const isVisible = ref(false)

const features = [
  {
    icon: MessageSquare,
    title: 'Pengembangan Berbasis Prompt',
    description: 'Bangun aplikasi dengan instruksi teks alami. Deskripsikan fitur atau tampilan dan AI akan menghasilkan kode secara otomatis dengan arsitektur yang bersih.',
    color: 'text-blue-600',
    category: 'AI Development'
  },
  {
    icon: Palette,
    title: 'Konversi Desain ke Kode',
    description: 'Upload desain dari Figma atau Sketch dan langsung konversi menjadi komponen React, Vue, Tailwind, atau Flutter yang siap produksi.',
    color: 'text-purple-600',
    category: 'Design Tools'
  },
  {
    icon: Brain,
    title: 'AI Frontend Engineer',
    description: 'Optimasi UI/UX otomatis dengan React modern, Next.js, Vue 3, Tailwind CSS, dan TypeScript. Local-first untuk keamanan maksimal.',
    color: 'text-indigo-600',
    category: 'AI Development'
  },
  {
    icon: Database,
    title: 'Integrasi Full-Stack',
    description: 'Backend otomatis melalui Supabase: database PostgreSQL, autentikasi, penyimpanan file, dan realtime subscriptions. API auto-generated berdasarkan prompt.',
    color: 'text-green-600',
    category: 'Backend'
  },
  {
    icon: Eye,
    title: 'Visual Editing & Live Preview',
    description: 'Edit teks, layout, dan media langsung di browser dengan live preview. Perubahan tersinkron secara real-time dengan source code.',
    color: 'text-orange-600',
    category: 'Development Tools'
  },
  {
    icon: Layout,
    title: 'Template Siap Pakai',
    description: 'Landing page, aplikasi SaaS, dokumentasi, sistem catatan, dashboard admin, e-commerce. Pilih template, kustomisasi via prompt.',
    color: 'text-pink-600',
    category: 'Templates'
  },
  {
    icon: Users,
    title: 'Kolaborasi Tim',
    description: 'Import repo tim dan lanjutkan pengembangan bersama. Workflow developer lengkap: pull request, branch, merge via GitHub integration.',
    color: 'text-cyan-600',
    category: 'Collaboration'
  },
  {
    icon: Rocket,
    title: 'Production-Ready & Scalable',
    description: 'Kode output yang bersih dan modular dengan best practices. Deploy ke Vercel, Netlify, AWS, atau server cloud mana pun dengan mudah.',
    color: 'text-red-600',
    category: 'Deployment'
  },
  {
    icon: Shield,
    title: 'Keamanan Enterprise',
    description: 'Enkripsi end-to-end, audit trails, role-based access control, dan compliance GDPR. Data Anda aman dengan sertifikasi SOC 2.',
    color: 'text-gray-600',
    category: 'Security'
  },
  {
    icon: Zap,
    title: 'Performance Optimization',
    description: 'Code splitting otomatis, lazy loading, optimasi gambar, dan caching strategis. Aplikasi Anda akan super cepat dan responsif.',
    color: 'text-yellow-600',
    category: 'Performance'
  },
  {
    icon: Code,
    title: 'Multi-Framework Support',
    description: 'Dukung React, Vue, Angular, Svelte, Next.js, Nuxt.js, dan Flutter. Pilih framework favorit Anda atau biarkan AI merekomendasikan.',
    color: 'text-purple-500',
    category: 'Frameworks'
  },
  {
    icon: Globe,
    title: 'Internationalization',
    description: 'Dukungan multi-bahasa built-in dengan i18n routing, RTL support, dan lokalisasi konten otomatis untuk jangkauan global.',
    color: 'text-blue-500',
    category: 'Localization'
  }
]

onMounted(() => {
  const observer = new IntersectionObserver((entries) => {
    entries.forEach((entry) => {
      if (entry.isIntersecting) {
        isVisible.value = true
      }
    })
  })
  
  const element = document.getElementById('features')
  if (element) {
    observer.observe(element)
  }
})
</script>

<template>
  <section id="features" class="py-20 bg-white dark:bg-gray-900">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="text-center mb-16">
        <h2 class="text-4xl md:text-5xl font-bold mb-4">
          <span class="gradient-text">Fitur-Fitur Canggih</span>
        </h2>
        <p class="text-xl text-gray-600 dark:text-gray-300 max-w-3xl mx-auto">
          Semua yang Anda butuhkan untuk membangun, menerapkan, dan menskalakan aplikasi modern dengan bantuan AI
        </p>
      </div>

      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
        <div 
          v-for="(feature, index) in features" 
          :key="feature.title"
          :class="[
            'feature-card transition-all duration-700 group',
            isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10'
          ]"
          :style="{ transitionDelay: `${index * 100}ms` }"
        >
          <div class="flex items-start justify-between mb-4">
            <div :class="['p-3 rounded-lg bg-gray-100 dark:bg-gray-800 group-hover:scale-110 transition-transform', feature.color]">
              <component :is="feature.icon" class="h-6 w-6" />
            </div>
            <span class="text-xs px-2 py-1 bg-gray-100 dark:bg-gray-800 rounded-full text-gray-600 dark:text-gray-400">
              {{ feature.category }}
            </span>
          </div>
          <h3 class="text-xl font-semibold mb-3 text-gray-900 dark:text-white group-hover:text-blue-600 transition-colors">
            {{ feature.title }}
          </h3>
          <p class="text-gray-600 dark:text-gray-300 leading-relaxed">
            {{ feature.description }}
          </p>
        </div>
      </div>
    </div>
  </section>
</template>
