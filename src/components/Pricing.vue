<script setup lang="ts">
import { ref, onMounted } from 'vue'
import { Check, Zap, Crown, Building } from 'lucide-vue-next'
import SignupModal from './SignupModal.vue'

const isVisible = ref(false)
const billingCycle = ref<'monthly' | 'yearly'>('monthly')
const isSignupModalOpen = ref(false)

const plans = [
  {
    name: 'Starter',
    icon: Zap,
    description: 'Sempurna untuk individu dan project pribadi',
    monthlyPrice: 0,
    yearlyPrice: 0,
    popular: false,
    features: [
      '3 proyek aktif',
      '10 AI generations per bulan',
      'Template dasar',
      'Deployment ke Netlify/Vercel',
      'Community support',
      'Basic analytics'
    ],
    limitations: [
      'Branding AI Unified Builder',
      'Storage 1GB',
      'Bandwidth 10GB/bulan'
    ]
  },
  {
    name: 'Pro',
    icon: Crown,
    description: 'Untuk developer profesional dan startup',
    monthlyPrice: 29,
    yearlyPrice: 290,
    popular: true,
    features: [
      'Proyek unlimited',
      '500 AI generations per bulan',
      'Semua template premium',
      'Custom domains',
      'Advanced integrations',
      'Priority support',
      'Advanced analytics',
      'Team collaboration (5 anggota)',
      'Custom branding',
      'API access'
    ],
    limitations: [
      'Storage 50GB',
      'Bandwidth 500GB/bulan'
    ]
  },
  {
    name: 'Enterprise',
    icon: Building,
    description: 'Untuk tim besar dan organisasi',
    monthlyPrice: 99,
    yearlyPrice: 990,
    popular: false,
    features: [
      'Segala fitur Pro',
      'AI generations unlimited',
      'White-label solution',
      'SSO & SAML',
      'Advanced security',
      'Dedicated support',
      'Custom integrations',
      'Team unlimited',
      'Audit logs',
      'SLA 99.9%',
      'Custom training',
      'On-premise option'
    ],
    limitations: [
      'Storage 1TB',
      'Bandwidth unlimited'
    ]
  }
]

const faqs = [
  {
    question: 'Apakah ada free trial?',
    answer: 'Ya! Plan Starter gratis selamanya dengan batasan tertentu. Untuk Pro dan Enterprise, Anda bisa mencoba gratis selama 14 hari.'
  },
  {
    question: 'Bisakah saya upgrade/downgrade kapan saja?',
    answer: 'Tentu saja! Anda bisa mengubah plan kapan saja. Perubahan akan berlaku di cycle billing berikutnya.'
  },
  {
    question: 'Apakah kode yang dihasilkan bisa saya download?',
    answer: 'Ya, semua kode yang dihasilkan adalah milik Anda 100%. Anda bisa download dan deploy di mana saja.'
  },
  {
    question: 'Bagaimana dengan dukungan teknis?',
    answer: 'Kami menyediakan community support untuk Starter, priority support untuk Pro, dan dedicated support untuk Enterprise.'
  }
]

const handleSignup = (data: { name: string; email: string; password: string }) => {
  console.log('User signed up:', data)
  // Here you would integrate with Supabase
}

const selectPlan = (planName: string) => {
  console.log('Selected plan:', planName)
  if (planName === 'Starter') {
    isSignupModalOpen.value = true
  } else if (planName === 'Enterprise') {
    // Open contact sales modal or redirect
    window.open('mailto:sales@aiunifiedbuilder.com?subject=Enterprise Plan Inquiry', '_blank')
  } else {
    isSignupModalOpen.value = true
  }
}

onMounted(() => {
  const observer = new IntersectionObserver((entries) => {
    entries.forEach((entry) => {
      if (entry.isIntersecting) {
        isVisible.value = true
      }
    })
  })
  
  const element = document.getElementById('pricing')
  if (element) {
    observer.observe(element)
  }
})
</script>

<template>
  <section id="pricing" class="py-20 gradient-bg">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="text-center mb-16">
        <h2 class="text-4xl md:text-5xl font-bold mb-4">
          <span class="gradient-text">Harga Yang Transparan</span>
        </h2>
        <p class="text-xl text-gray-600 dark:text-gray-300 max-w-3xl mx-auto mb-8">
          Pilih plan yang sesuai dengan kebutuhan Anda. Mulai gratis, upgrade kapan saja.
        </p>
        
        <!-- Billing Toggle -->
        <div class="flex items-center justify-center mb-8">
          <span :class="['mr-3', billingCycle === 'monthly' ? 'text-gray-900 dark:text-white font-semibold' : 'text-gray-500']">
            Bulanan
          </span>
          <button 
            @click="billingCycle = billingCycle === 'monthly' ? 'yearly' : 'monthly'"
            class="relative inline-flex h-6 w-11 items-center rounded-full bg-gray-200 dark:bg-gray-700 transition-colors focus:outline-none focus:ring-2 focus:ring-blue-500 focus:ring-offset-2"
          >
            <span 
              :class="[
                'inline-block h-4 w-4 transform rounded-full bg-white transition-transform',
                billingCycle === 'yearly' ? 'translate-x-6' : 'translate-x-1'
              ]"
            />
          </button>
          <span :class="['ml-3', billingCycle === 'yearly' ? 'text-gray-900 dark:text-white font-semibold' : 'text-gray-500']">
            Tahunan
          </span>
          <span v-if="billingCycle === 'yearly'" class="ml-2 px-2 py-1 bg-green-100 text-green-800 text-sm rounded-full">
            Hemat 20%
          </span>
        </div>
      </div>

      <!-- Pricing Cards -->
      <div class="grid grid-cols-1 md:grid-cols-3 gap-8 mb-16">
        <div 
          v-for="(plan, index) in plans" 
          :key="plan.name"
          :class="[
            'relative feature-card transition-all duration-700',
            plan.popular ? 'ring-2 ring-blue-500 scale-105' : '',
            isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10'
          ]"
          :style="{ transitionDelay: `${index * 200}ms` }"
        >
          <!-- Popular Badge -->
          <div v-if="plan.popular" class="absolute -top-4 left-1/2 transform -translate-x-1/2">
            <span class="bg-blue-600 text-white px-4 py-1 rounded-full text-sm font-semibold">
              Terpopuler
            </span>
          </div>

          <div class="text-center mb-6">
            <div :class="['inline-flex p-3 rounded-lg mb-4', plan.popular ? 'bg-blue-600 text-white' : 'bg-gray-100 dark:bg-gray-800 text-gray-600 dark:text-gray-300']">
              <component :is="plan.icon" class="h-8 w-8" />
            </div>
            <h3 class="text-2xl font-bold text-gray-900 dark:text-white mb-2">{{ plan.name }}</h3>
            <p class="text-gray-600 dark:text-gray-300 mb-4">{{ plan.description }}</p>
            
            <div class="text-4xl font-bold text-gray-900 dark:text-white">
              <span v-if="billingCycle === 'monthly'">
                {{ plan.monthlyPrice === 0 ? 'Gratis' : `$${plan.monthlyPrice}` }}
              </span>
              <span v-else>
                {{ plan.yearlyPrice === 0 ? 'Gratis' : `$${Math.round(plan.yearlyPrice / 12)}` }}
              </span>
              <span v-if="plan.monthlyPrice > 0" class="text-lg font-normal text-gray-500">
                /{{ billingCycle === 'monthly' ? 'bulan' : 'bulan' }}
              </span>
            </div>
            <p v-if="billingCycle === 'yearly' && plan.yearlyPrice > 0" class="text-sm text-gray-500 mt-1">
              Ditagih ${{ plan.yearlyPrice }} per tahun
            </p>
          </div>

          <!-- Features -->
          <div class="space-y-3 mb-6">
            <div v-for="feature in plan.features" :key="feature" class="flex items-start space-x-3">
              <Check class="h-5 w-5 text-green-500 flex-shrink-0 mt-0.5" />
              <span class="text-gray-700 dark:text-gray-300">{{ feature }}</span>
            </div>
          </div>

          <!-- Limitations -->
          <div v-if="plan.limitations.length > 0" class="border-t border-gray-200 dark:border-gray-700 pt-4 mb-6">
            <p class="text-sm font-medium text-gray-500 mb-2">Batasan:</p>
            <div class="space-y-1">
              <div v-for="limitation in plan.limitations" :key="limitation" class="text-sm text-gray-500">
                • {{ limitation }}
              </div>
            </div>
          </div>

          <!-- CTA Button -->
          <button 
            @click="selectPlan(plan.name)"
            :class="[
              'w-full py-3 px-6 rounded-xl font-semibold transition-all duration-300',
              plan.popular 
                ? 'bg-blue-600 hover:bg-blue-700 text-white shadow-lg hover:shadow-xl' 
                : 'border-2 border-gray-300 dark:border-gray-600 text-gray-700 dark:text-gray-300 hover:border-blue-600 hover:text-blue-600'
            ]"
          >
            {{ plan.name === 'Starter' ? 'Mulai Gratis' : plan.name === 'Enterprise' ? 'Hubungi Sales' : 'Mulai Trial 14 Hari' }}
          </button>
        </div>
      </div>

      <!-- FAQ -->
      <div class="max-w-3xl mx-auto">
        <h3 class="text-2xl font-bold text-center mb-8 text-gray-900 dark:text-white">
          Pertanyaan yang Sering Diajukan
        </h3>
        <div class="space-y-4">
          <div v-for="faq in faqs" :key="faq.question" class="feature-card">
            <h4 class="font-semibold text-gray-900 dark:text-white mb-2">{{ faq.question }}</h4>
            <p class="text-gray-600 dark:text-gray-300">{{ faq.answer }}</p>
          </div>
        </div>
      </div>
    </div>

    <!-- Signup Modal -->
    <SignupModal 
      :is-open="isSignupModalOpen"
      @close="isSignupModalOpen = false"
      @signup="handleSignup"
    />
  </section>
</template>
