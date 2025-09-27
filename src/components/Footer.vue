<script setup lang="ts">
import { Sparkles, Github, Twitter, Linkedin, Mail, Phone, MapPin } from 'lucide-vue-next'

const quickLinks = [
  { name: 'Fitur', href: '#features' },
  { name: 'Demo', href: '#demo' },
  { name: 'Integrasi', href: '#integrations' },
  { name: 'Harga', href: '#pricing' },
  { name: 'Testimoni', href: '#testimonials' }
]

const resources = [
  { name: 'Dokumentasi', href: '#' },
  { name: 'API Reference', href: '#' },
  { name: 'Tutorial', href: '#' },
  { name: 'Blog', href: '#' },
  { name: 'Community', href: '#' }
]

const support = [
  { name: 'Help Center', href: '#' },
  { name: 'Hubungi Kami', href: '#' },
  { name: 'Status System', href: '#' },
  { name: 'Lapor Bug', href: '#' },
  { name: 'Feature Request', href: '#' }
]

const company = [
  { name: 'Tentang Kami', href: '#' },
  { name: 'Karir', href: '#' },
  { name: 'Press Kit', href: '#' },
  { name: 'Partner', href: '#' },
  { name: 'Investor', href: '#' }
]
</script>

<template>
  <footer class="bg-gray-900 text-white py-16">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-6 gap-8">
        <!-- Logo & Description -->
        <div class="lg:col-span-2">
          <div class="flex items-center space-x-2 mb-4">
            <Sparkles class="h-8 w-8 text-blue-400" />
            <span class="text-xl font-bold">AI Unified Builder</span>
          </div>
          <p class="text-gray-400 mb-6 max-w-md">
            Platform bertenaga AI paling canggih untuk membangun aplikasi web dan mobile. 
            Transformasikan ide Anda menjadi aplikasi siap produksi dalam hitungan menit.
          </p>
          
          <!-- Contact Info -->
          <div class="space-y-2 mb-6">
            <div class="flex items-center space-x-2 text-gray-400">
              <Mail class="h-4 w-4" />
              <span class="text-sm">support@aiunifiedbuilder.com</span>
            </div>
            <div class="flex items-center space-x-2 text-gray-400">
              <Phone class="h-4 w-4" />
              <span class="text-sm">+62 21 1234 5678</span>
            </div>
            <div class="flex items-center space-x-2 text-gray-400">
              <MapPin class="h-4 w-4" />
              <span class="text-sm">Jakarta, Indonesia</span>
            </div>
          </div>

          <!-- Social Links -->
          <div class="flex space-x-4">
            <a href="#" class="text-gray-400 hover:text-blue-400 transition-colors">
              <Github class="h-6 w-6" />
            </a>
            <a href="#" class="text-gray-400 hover:text-blue-400 transition-colors">
              <Twitter class="h-6 w-6" />
            </a>
            <a href="#" class="text-gray-400 hover:text-blue-400 transition-colors">
              <Linkedin class="h-6 w-6" />
            </a>
            <a href="#" class="text-gray-400 hover:text-blue-400 transition-colors">
              <Mail class="h-6 w-6" />
            </a>
          </div>
        </div>

        <!-- Quick Links -->
        <div>
          <h3 class="text-lg font-semibold mb-4">Quick Links</h3>
          <ul class="space-y-2">
            <li v-for="link in quickLinks" :key="link.name">
              <a :href="link.href" class="text-gray-400 hover:text-white transition-colors">
                {{ link.name }}
              </a>
            </li>
          </ul>
        </div>

        <!-- Resources -->
        <div>
          <h3 class="text-lg font-semibold mb-4">Resources</h3>
          <ul class="space-y-2">
            <li v-for="resource in resources" :key="resource.name">
              <a :href="resource.href" class="text-gray-400 hover:text-white transition-colors">
                {{ resource.name }}
              </a>
            </li>
          </ul>
        </div>

        <!-- Support -->
        <div>
          <h3 class="text-lg font-semibold mb-4">Support</h3>
          <ul class="space-y-2">
            <li v-for="item in support" :key="item.name">
              <a :href="item.href" class="text-gray-400 hover:text-white transition-colors">
                {{ item.name }}
              </a>
            </li>
          </ul>
        </div>

        <!-- Company -->
        <div>
          <h3 class="text-lg font-semibold mb-4">Company</h3>
          <ul class="space-y-2">
            <li v-for="item in company" :key="item.name">
              <a :href="item.href" class="text-gray-400 hover:text-white transition-colors">
                {{ item.name }}
              </a>
            </li>
          </ul>
        </div>
      </div>

      <!-- Newsletter Signup -->
      <div class="border-t border-gray-800 mt-12 pt-8">
        <div class="max-w-md mx-auto text-center mb-8">
          <h4 class="text-lg font-semibold mb-2">Subscribe Newsletter</h4>
          <p class="text-gray-400 text-sm mb-4">Dapatkan update terbaru tentang fitur dan tips pengembangan</p>
          <div class="flex">
            <input 
              type="email" 
              placeholder="Masukkan email Anda"
              class="flex-1 px-4 py-2 bg-gray-800 border border-gray-700 rounded-l-lg text-white placeholder-gray-400 focus:outline-none focus:ring-2 focus:ring-blue-500"
            />
            <button class="bg-blue-600 hover:bg-blue-700 px-6 py-2 rounded-r-lg transition-colors">
              Subscribe
            </button>
          </div>
        </div>
      </div>

      <!-- Bottom Section -->
      <div class="border-t border-gray-800 pt-8 flex flex-col md:flex-row justify-between items-center">
        <p class="text-gray-400 text-sm">
          © 2025 AI Unified Builder. All rights reserved.
        </p>
        <div class="flex space-x-6 mt-4 md:mt-0">
          <a href="#" class="text-gray-400 hover:text-white transition-colors text-sm">Privacy Policy</a>
          <a href="#" class="text-gray-400 hover:text-white transition-colors text-sm">Terms of Service</a>
          <a href="#" class="text-gray-400 hover:text-white transition-colors text-sm">Cookie Policy</a>
          <a href="#" class="text-gray-400 hover:text-white transition-colors text-sm">GDPR</a>
        </div>
      </div>

      <!-- Made in Indonesia -->
      <div class="text-center mt-6">
        <span class="text-gray-500 text-sm">
          🇮🇩 Proudly made in Indonesia with ❤️
        </span>
      </div>
    </div>
  </footer>
</template>
