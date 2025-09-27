<script setup lang="ts">
import { ref, computed } from 'vue'
import { X, Mail, Lock, User, Eye, EyeOff, CheckCircle, ArrowRight, Github } from 'lucide-vue-next'

const props = defineProps<{
  isOpen: boolean
}>()

const emit = defineEmits<{
  close: []
  signup: [data: { name: string; email: string; password: string }]
}>()

const currentStep = ref(1)
const isLoading = ref(false)
const showPassword = ref(false)
const acceptTerms = ref(false)

const formData = ref({
  name: '',
  email: '',
  password: '',
  confirmPassword: ''
})

const errors = ref({
  name: '',
  email: '',
  password: '',
  confirmPassword: '',
  terms: ''
})

const isFormValid = computed(() => {
  return formData.value.name.length >= 2 &&
         isValidEmail(formData.value.email) &&
         formData.value.password.length >= 8 &&
         formData.value.password === formData.value.confirmPassword &&
         acceptTerms.value
})

const isValidEmail = (email: string) => {
  return /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email)
}

const validateForm = () => {
  errors.value = {
    name: '',
    email: '',
    password: '',
    confirmPassword: '',
    terms: ''
  }

  if (formData.value.name.length < 2) {
    errors.value.name = 'Nama minimal 2 karakter'
  }

  if (!isValidEmail(formData.value.email)) {
    errors.value.email = 'Format email tidak valid'
  }

  if (formData.value.password.length < 8) {
    errors.value.password = 'Password minimal 8 karakter'
  }

  if (formData.value.password !== formData.value.confirmPassword) {
    errors.value.confirmPassword = 'Password tidak cocok'
  }

  if (!acceptTerms.value) {
    errors.value.terms = 'Anda harus menyetujui syarat dan ketentuan'
  }

  return Object.values(errors.value).every(error => error === '')
}

const handleSignup = async () => {
  if (!validateForm()) return

  isLoading.value = true
  
  try {
    // Simulate API call - replace with actual Supabase integration
    await new Promise(resolve => setTimeout(resolve, 2000))
    
    emit('signup', {
      name: formData.value.name,
      email: formData.value.email,
      password: formData.value.password
    })
    
    currentStep.value = 2
  } catch (error) {
    console.error('Signup error:', error)
  } finally {
    isLoading.value = false
  }
}

const socialSignup = (provider: string) => {
  // Placeholder for social auth - integrate with Supabase
  console.log(`Sign up with ${provider}`)
}

const resetForm = () => {
  currentStep.value = 1
  formData.value = {
    name: '',
    email: '',
    password: '',
    confirmPassword: ''
  }
  acceptTerms.value = false
  errors.value = {
    name: '',
    email: '',
    password: '',
    confirmPassword: '',
    terms: ''
  }
}

const handleClose = () => {
  resetForm()
  emit('close')
}
</script>

<template>
  <Teleport to="body">
    <div v-if="isOpen" class="fixed inset-0 z-50 flex items-center justify-center">
      <!-- Backdrop -->
      <div 
        class="absolute inset-0 bg-black/50 backdrop-blur-sm"
        @click="handleClose"
      ></div>
      
      <!-- Modal -->
      <div class="relative bg-white dark:bg-gray-800 rounded-2xl shadow-2xl max-w-md w-full mx-4 max-h-[90vh] overflow-y-auto">
        <!-- Close Button -->
        <button 
          @click="handleClose"
          class="absolute top-4 right-4 p-2 text-gray-400 hover:text-gray-600 dark:hover:text-gray-200 transition-colors z-10"
        >
          <X class="h-5 w-5" />
        </button>

        <!-- Step 1: Registration Form -->
        <div v-if="currentStep === 1" class="p-8">
          <div class="text-center mb-8">
            <h2 class="text-2xl font-bold text-gray-900 dark:text-white mb-2">
              🚀 Mulai Membangun Sekarang
            </h2>
            <p class="text-gray-600 dark:text-gray-300">
              Bergabung dengan 50K+ developer dan mulai membangun aplikasi impian Anda
            </p>
          </div>

          <form @submit.prevent="handleSignup" class="space-y-4">
            <!-- Name Input -->
            <div>
              <label class="block text-sm font-medium text-gray-700 dark:text-gray-300 mb-2">
                Nama Lengkap
              </label>
              <div class="relative">
                <User class="absolute left-3 top-1/2 transform -translate-y-1/2 h-5 w-5 text-gray-400" />
                <input
                  v-model="formData.name"
                  type="text"
                  placeholder="Masukkan nama lengkap"
                  :class="[
                    'w-full pl-10 pr-4 py-3 border rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500 dark:bg-gray-700 dark:border-gray-600 dark:text-white transition-colors',
                    errors.name ? 'border-red-500' : 'border-gray-300'
                  ]"
                />
              </div>
              <p v-if="errors.name" class="text-red-500 text-sm mt-1">{{ errors.name }}</p>
            </div>

            <!-- Email Input -->
            <div>
              <label class="block text-sm font-medium text-gray-700 dark:text-gray-300 mb-2">
                Email
              </label>
              <div class="relative">
                <Mail class="absolute left-3 top-1/2 transform -translate-y-1/2 h-5 w-5 text-gray-400" />
                <input
                  v-model="formData.email"
                  type="email"
                  placeholder="nama@perusahaan.com"
                  :class="[
                    'w-full pl-10 pr-4 py-3 border rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500 dark:bg-gray-700 dark:border-gray-600 dark:text-white transition-colors',
                    errors.email ? 'border-red-500' : 'border-gray-300'
                  ]"
                />
              </div>
              <p v-if="errors.email" class="text-red-500 text-sm mt-1">{{ errors.email }}</p>
            </div>

            <!-- Password Input -->
            <div>
              <label class="block text-sm font-medium text-gray-700 dark:text-gray-300 mb-2">
                Password
              </label>
              <div class="relative">
                <Lock class="absolute left-3 top-1/2 transform -translate-y-1/2 h-5 w-5 text-gray-400" />
                <input
                  v-model="formData.password"
                  :type="showPassword ? 'text' : 'password'"
                  placeholder="Minimal 8 karakter"
                  :class="[
                    'w-full pl-10 pr-12 py-3 border rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500 dark:bg-gray-700 dark:border-gray-600 dark:text-white transition-colors',
                    errors.password ? 'border-red-500' : 'border-gray-300'
                  ]"
                />
                <button
                  type="button"
                  @click="showPassword = !showPassword"
                  class="absolute right-3 top-1/2 transform -translate-y-1/2 text-gray-400 hover:text-gray-600"
                >
                  <Eye v-if="showPassword" class="h-5 w-5" />
                  <EyeOff v-else class="h-5 w-5" />
                </button>
              </div>
              <p v-if="errors.password" class="text-red-500 text-sm mt-1">{{ errors.password }}</p>
            </div>

            <!-- Confirm Password Input -->
            <div>
              <label class="block text-sm font-medium text-gray-700 dark:text-gray-300 mb-2">
                Konfirmasi Password
              </label>
              <div class="relative">
                <Lock class="absolute left-3 top-1/2 transform -translate-y-1/2 h-5 w-5 text-gray-400" />
                <input
                  v-model="formData.confirmPassword"
                  type="password"
                  placeholder="Ulangi password"
                  :class="[
                    'w-full pl-10 pr-4 py-3 border rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500 dark:bg-gray-700 dark:border-gray-600 dark:text-white transition-colors',
                    errors.confirmPassword ? 'border-red-500' : 'border-gray-300'
                  ]"
                />
              </div>
              <p v-if="errors.confirmPassword" class="text-red-500 text-sm mt-1">{{ errors.confirmPassword }}</p>
            </div>

            <!-- Terms & Conditions -->
            <div class="flex items-start space-x-3">
              <input
                v-model="acceptTerms"
                type="checkbox"
                id="terms"
                class="mt-1 h-4 w-4 text-blue-600 focus:ring-blue-500 border-gray-300 rounded"
              />
              <label for="terms" class="text-sm text-gray-600 dark:text-gray-300">
                Saya menyetujui <a href="#" class="text-blue-600 hover:underline">Syarat & Ketentuan</a> 
                dan <a href="#" class="text-blue-600 hover:underline">Kebijakan Privasi</a>
              </label>
            </div>
            <p v-if="errors.terms" class="text-red-500 text-sm">{{ errors.terms }}</p>

            <!-- Submit Button -->
            <button
              type="submit"
              :disabled="!isFormValid || isLoading"
              :class="[
                'w-full py-3 px-4 rounded-lg font-semibold transition-all duration-300 flex items-center justify-center space-x-2',
                isFormValid && !isLoading
                  ? 'bg-blue-600 hover:bg-blue-700 text-white shadow-lg hover:shadow-xl'
                  : 'bg-gray-300 dark:bg-gray-600 text-gray-500 cursor-not-allowed'
              ]"
            >
              <span v-if="isLoading">Mendaftarkan...</span>
              <span v-else>Daftar Gratis</span>
              <ArrowRight v-if="!isLoading" class="h-5 w-5" />
            </button>
          </form>

          <!-- Social Sign Up -->
          <div class="mt-6">
            <div class="relative">
              <div class="absolute inset-0 flex items-center">
                <div class="w-full border-t border-gray-300 dark:border-gray-600"></div>
              </div>
              <div class="relative flex justify-center text-sm">
                <span class="px-2 bg-white dark:bg-gray-800 text-gray-500">Atau daftar dengan</span>
              </div>
            </div>

            <div class="mt-4 grid grid-cols-2 gap-3">
              <button
                @click="socialSignup('google')"
                class="flex items-center justify-center px-4 py-2 border border-gray-300 dark:border-gray-600 rounded-lg hover:bg-gray-50 dark:hover:bg-gray-700 transition-colors"
              >
                <svg class="h-5 w-5 mr-2" viewBox="0 0 24 24">
                  <path fill="#4285F4" d="M22.56 12.25c0-.78-.07-1.53-.2-2.25H12v4.26h5.92c-.26 1.37-1.04 2.53-2.21 3.31v2.77h3.57c2.08-1.92 3.28-4.74 3.28-8.09z"/>
                  <path fill="#34A853" d="M12 23c2.97 0 5.46-.98 7.28-2.66l-3.57-2.77c-.98.66-2.23 1.06-3.71 1.06-2.86 0-5.29-1.93-6.16-4.53H2.18v2.84C3.99 20.53 7.7 23 12 23z"/>
                  <path fill="#FBBC05" d="M5.84 14.09c-.22-.66-.35-1.36-.35-2.09s.13-1.43.35-2.09V7.07H2.18C1.43 8.55 1 10.22 1 12s.43 3.45 1.18 4.93l2.85-2.22.81-.62z"/>
                  <path fill="#EA4335" d="M12 5.38c1.62 0 3.06.56 4.21 1.64l3.15-3.15C17.45 2.09 14.97 1 12 1 7.7 1 3.99 3.47 2.18 7.07l3.66 2.84c.87-2.6 3.3-4.53 6.16-4.53z"/>
                </svg>
                Google
              </button>
              <button
                @click="socialSignup('github')"
                class="flex items-center justify-center px-4 py-2 border border-gray-300 dark:border-gray-600 rounded-lg hover:bg-gray-50 dark:hover:bg-gray-700 transition-colors"
              >
                <Github class="h-5 w-5 mr-2" />
                GitHub
              </button>
            </div>
          </div>

          <!-- Login Link -->
          <p class="text-center text-sm text-gray-600 dark:text-gray-300 mt-6">
            Sudah punya akun? 
            <a href="#" class="text-blue-600 hover:underline font-medium">Masuk di sini</a>
          </p>
        </div>

        <!-- Step 2: Success -->
        <div v-if="currentStep === 2" class="p-8 text-center">
          <div class="mb-6">
            <div class="w-16 h-16 bg-green-100 dark:bg-green-900/20 rounded-full flex items-center justify-center mx-auto mb-4">
              <CheckCircle class="h-8 w-8 text-green-600" />
            </div>
            <h2 class="text-2xl font-bold text-gray-900 dark:text-white mb-2">
              🎉 Selamat Datang!
            </h2>
            <p class="text-gray-600 dark:text-gray-300 mb-6">
              Akun Anda telah berhasil dibuat. Silakan cek email untuk verifikasi.
            </p>
          </div>

          <div class="space-y-4">
            <button
              @click="handleClose"
              class="w-full bg-blue-600 hover:bg-blue-700 text-white py-3 px-4 rounded-lg font-semibold transition-all duration-300"
            >
              Mulai Membangun Aplikasi
            </button>
            <button
              @click="handleClose"
              class="w-full border-2 border-gray-300 dark:border-gray-600 text-gray-700 dark:text-gray-300 hover:border-blue-600 hover:text-blue-600 py-3 px-4 rounded-lg font-semibold transition-all duration-300"
            >
              Lihat Tutorial
            </button>
          </div>

          <div class="mt-6 p-4 bg-blue-50 dark:bg-blue-900/20 rounded-lg">
            <h4 class="font-semibold text-blue-900 dark:text-blue-100 mb-2">Langkah Selanjutnya:</h4>
            <ul class="text-sm text-blue-800 dark:text-blue-200 space-y-1">
              <li>✓ Verifikasi email Anda</li>
              <li>✓ Lengkapi profil</li>
              <li>✓ Pilih template pertama</li>
              <li>✓ Mulai membangun!</li>
            </ul>
          </div>
        </div>
      </div>
    </div>
  </Teleport>
</template>
