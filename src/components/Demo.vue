<script setup lang="ts">
import { ref, onMounted } from 'vue'
import { Terminal, Code, Smartphone, Monitor, CheckCircle } from 'lucide-vue-next'

const isVisible = ref(false)
const currentStep = ref(0)
const prompt = ref('')
const isTyping = ref(false)

const demoSteps = [
  {
    icon: Terminal,
    title: 'Masukkan Prompt Anda',
    description: 'Deskripsikan apa yang ingin Anda bangun',
    prompt: 'Buat aplikasi catatan dengan login, upload gambar, dan berbagi publik',
    color: 'bg-blue-600'
  },
  {
    icon: Code,
    title: 'AI Menghasilkan Kode',
    description: 'Aplikasi React + Supabase lengkap',
    prompt: 'Membuat komponen, autentikasi, dan skema database...',
    color: 'bg-green-600'
  },
  {
    icon: Smartphone,
    title: 'Desain Responsif',
    description: 'Bekerja sempurna di semua perangkat',
    prompt: 'Menerapkan utilitas responsif Tailwind CSS...',
    color: 'bg-purple-600'
  },
  {
    icon: Monitor,
    title: 'Siap Deploy',
    description: 'Aplikasi siap produksi',
    prompt: 'Aplikasi Anda siap! Deploy ke Vercel atau Netlify.',
    color: 'bg-indigo-600'
  }
]

const features = [
  'Kode bersih dan terstruktur',
  'Best practices otomatis',
  'SEO optimized',
  'Responsive design',
  'Error handling',
  'Loading states'
]

const typeWriter = (text: string, callback?: () => void) => {
  isTyping.value = true
  prompt.value = ''
  let i = 0
  const timer = setInterval(() => {
    if (i < text.length) {
      prompt.value += text.charAt(i)
      i++
    } else {
      clearInterval(timer)
      isTyping.value = false
      if (callback) callback()
    }
  }, 50)
}

const nextStep = () => {
  if (currentStep.value < demoSteps.length - 1) {
    currentStep.value++
    typeWriter(demoSteps[currentStep.value].prompt, () => {
      setTimeout(nextStep, 3000)
    })
  } else {
    setTimeout(() => {
      currentStep.value = 0
      typeWriter(demoSteps[0].prompt, () => {
        setTimeout(nextStep, 3000)
      })
    }, 3000)
  }
}

onMounted(() => {
  const observer = new IntersectionObserver((entries) => {
    entries.forEach((entry) => {
      if (entry.isIntersecting) {
        isVisible.value = true
        setTimeout(() => {
          typeWriter(demoSteps[0].prompt, () => {
            setTimeout(nextStep, 3000)
          })
        }, 1000)
      }
    })
  })
  
  const element = document.getElementById('demo')
  if (element) {
    observer.observe(element)
  }
})
</script>

<template>
  <section id="demo" class="py-20 gradient-bg">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="text-center mb-16">
        <h2 class="text-4xl md:text-5xl font-bold mb-4">
          <span class="gradient-text">Lihat Langsung Dalam Aksi</span>
        </h2>
        <p class="text-xl text-gray-600 dark:text-gray-300 max-w-3xl mx-auto">
          Saksikan bagaimana AI mengubah ide Anda menjadi aplikasi siap produksi dalam hitungan menit
        </p>
      </div>

      <div class="grid grid-cols-1 lg:grid-cols-2 gap-12 items-start">
        <!-- Demo Terminal -->
        <div 
          :class="[
            'bg-gray-900 rounded-2xl p-6 shadow-2xl transition-all duration-1000',
            isVisible ? 'opacity-100 translate-x-0' : 'opacity-0 -translate-x-10'
          ]"
        >
          <div class="flex items-center space-x-2 mb-4">
            <div class="w-3 h-3 bg-red-500 rounded-full"></div>
            <div class="w-3 h-3 bg-yellow-500 rounded-full"></div>
            <div class="w-3 h-3 bg-green-500 rounded-full"></div>
            <span class="text-gray-400 text-sm ml-4">Terminal AI Builder</span>
          </div>
          <div class="text-green-400 font-mono text-sm space-y-2 min-h-[120px]">
            <div class="flex items-start">
              <span class="text-blue-400 mr-2">$</span>
              <div class="flex-1">
                <span>{{ prompt }}</span>
                <span v-if="isTyping" class="animate-pulse ml-1">|</span>
              </div>
            </div>
            <div v-if="currentStep > 0" class="text-gray-500">
              <div class="flex items-center space-x-2 mt-2">
                <CheckCircle class="h-4 w-4 text-green-500" />
                <span>Komponen dibuat: 12 files</span>
              </div>
              <div class="flex items-center space-x-2">
                <CheckCircle class="h-4 w-4 text-green-500" />
                <span>Database schema: 5 tables</span>
              </div>
              <div class="flex items-center space-x-2">
                <CheckCircle class="h-4 w-4 text-green-500" />
                <span>API endpoints: 8 routes</span>
              </div>
            </div>
          </div>
        </div>

        <!-- Steps & Features -->
        <div 
          :class="[
            'space-y-6 transition-all duration-1000 delay-300',
            isVisible ? 'opacity-100 translate-x-0' : 'opacity-0 translate-x-10'
          ]"
        >
          <!-- Steps -->
          <div class="space-y-4">
            <div 
              v-for="(step, index) in demoSteps" 
              :key="step.title"
              :class="[
                'flex items-start space-x-4 p-4 rounded-xl transition-all duration-500',
                currentStep === index 
                  ? 'bg-blue-50 dark:bg-blue-900/20 border-2 border-blue-200 dark:border-blue-800 scale-105' 
                  : 'bg-white/50 dark:bg-gray-800/50 border border-gray-200 dark:border-gray-700'
              ]"
            >
              <div 
                :class="[
                  'p-3 rounded-lg transition-all duration-300 text-white',
                  currentStep === index ? step.color : 'bg-gray-100 dark:bg-gray-700 text-gray-600 dark:text-gray-300'
                ]"
              >
                <component :is="step.icon" class="h-6 w-6" />
              </div>
              <div>
                <h3 :class="[
                  'text-lg font-semibold transition-colors duration-300',
                  currentStep === index ? 'text-blue-600' : 'text-gray-900 dark:text-white'
                ]">
                  {{ step.title }}
                </h3>
                <p class="text-gray-600 dark:text-gray-300">
                  {{ step.description }}
                </p>
              </div>
            </div>
          </div>

          <!-- Features -->
          <div class="bg-white/80 dark:bg-gray-800/80 backdrop-blur-sm rounded-xl p-6 border border-gray-200/50 dark:border-gray-700/50">
            <h4 class="font-semibold text-gray-900 dark:text-white mb-4">Yang Anda Dapatkan:</h4>
            <div class="grid grid-cols-2 gap-3">
              <div v-for="feature in features" :key="feature" class="flex items-center space-x-2">
                <CheckCircle class="h-4 w-4 text-green-500" />
                <span class="text-sm text-gray-600 dark:text-gray-300">{{ feature }}</span>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
