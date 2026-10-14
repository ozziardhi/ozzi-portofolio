<template>
  <section id="experience" class="py-20 px-6 max-w-6xl mx-auto relative overflow-hidden">
    <div class="text-center mb-20">
      <h2 class="text-3xl md:text-4xl font-bold font-mono text-purple-400 mb-2">
        // My Career & Education Journey
      </h2>
      <p class="text-gray-400 font-mono text-sm">
        ~ Tracking my professional path from past to present ~
      </p>
    </div>

    <!-- Garis Tengah Utama (Desktop) -->
    <div class="hidden md:block absolute left-1/2 top-40 bottom-12 w-0.5 border-l-2 border-dashed border-purple-500/40 -translate-x-1/2 z-0"></div>

    <div class="space-y-24 relative z-10">
      
      <!-- Loop Data Experience -->
      <div 
        v-for="(item, index) in experiences" 
        :key="index"
        class="flex flex-col md:flex-row items-center justify-between"
      >
        <!-- Jika index genap: Card di Kiri, Foto di Kanan -->
        <template v-if="index % 2 === 0">
          <!-- Sisi Kiri: Card -->
          <div class="md:w-[45%] w-full mb-6 md:mb-0 md:text-right">
            <span class="text-xs font-mono text-purple-400 bg-purple-950/50 px-3 py-1 rounded border border-purple-500/30">
              {{ item.period }}
            </span>
            <h3 class="text-xl font-bold text-white mt-2">{{ item.title }}</h3>
            <p class="text-purple-300 font-mono text-sm mb-3">{{ item.company }}</p>
            <ul class="retro-box bg-[#161b22] p-5 rounded-lg text-gray-300 text-sm space-y-2 text-left">
              <li v-for="(desc, dIdx) in item.descriptions" :key="dIdx">
                {{ desc }}
              </li>
            </ul>
          </div>
          
          <!-- Tengah: Titik Node -->
          <div class="hidden md:flex items-center justify-center w-8 h-8 rounded-full bg-[#0d1117] border-2 border-purple-400 z-10 shadow-[0_0_15px_#a855f7]"></div>
          
          <!-- Sisi Kanan: Foto Polaroid -->
          <div class="md:w-[45%] w-full flex justify-center md:justify-start">
            <div class="retro-box bg-white p-3 pb-6 rounded shadow-xl rotate-2 max-w-55">
              <!-- Jika item memiliki imageSrc (foto asli), tampilkan gambar. Jika tidak, tampilkan label teks -->
              <div class="w-full h-32 bg-purple-950 flex items-center justify-center text-purple-300 font-mono text-xs overflow-hidden border border-purple-300/30">
                <img v-if="item.imageSrc" :src="item.imageSrc" alt="Experience Photo" class="w-full h-full object-cover" />
                <span v-else>{{ item.imageLabel }}</span>
              </div>
              <p class="font-mono text-gray-800 text-xs text-center mt-3 font-bold">{{ item.imageCaption }}</p>
            </div>
          </div>
        </template>

        <!-- Jika index ganjil: Foto di Kiri, Card di Kanan -->
        <template v-else>
          <!-- Sisi Kiri: Foto Polaroid -->
          <div class="md:w-[45%] w-full flex justify-center md:justify-end mb-6 md:mb-0 order-2 md:order-1">
            <div class="retro-box bg-white p-3 pb-6 rounded shadow-xl -rotate-2 max-w-55">
              <div class="w-full h-32 bg-purple-950 flex items-center justify-center text-purple-300 font-mono text-xs overflow-hidden border border-purple-300/30">
                <img v-if="item.imageSrc" :src="item.imageSrc" alt="Experience Photo" class="w-full h-full object-cover" />
                <span v-else>{{ item.imageLabel }}</span>
              </div>
              <p class="font-mono text-gray-800 text-xs text-center mt-3 font-bold">{{ item.imageCaption }}</p>
            </div>
          </div>
          
          <!-- Tengah: Titik Node -->
          <div class="hidden md:flex items-center justify-center w-8 h-8 rounded-full bg-[#0d1117] border-2 border-purple-400 z-10 shadow-[0_0_15px_#a855f7] order-1 md:order-2"></div>
          
          <!-- Sisi Kanan: Card -->
          <div class="md:w-[45%] w-full order-3">
            <span class="text-xs font-mono text-purple-400 bg-purple-950/50 px-3 py-1 rounded border border-purple-500/30">
              {{ item.period }}
            </span>
            <h3 class="text-xl font-bold text-white mt-2">{{ item.title }}</h3>
            <p class="text-purple-300 font-mono text-sm mb-3">{{ item.company }}</p>
            <ul class="retro-box bg-[#161b22] p-5 rounded-lg text-gray-300 text-sm space-y-2">
              <li v-for="(desc, dIdx) in item.descriptions" :key="dIdx">
                {{ desc }}
              </li>
            </ul>
          </div>
        </template>

      </div>

    </div>
  </section>
</template>

<script setup>
import { ref } from 'vue'

// 1. IMPORT FOTO iSeller ANDA DI SINI
// (Pastikan file foto iSeller Anda disimpan di dalam folder src/assets/ dengan nama file yang sesuai)
import isellerImg from '../assets/iseller-pos.jpg'
import gudangImg from '../assets/gudang.jpg'
import unbhayangkaraImg from '../assets/wisuda.jpg'
import kalanaraImg from '../assets/kalanara.jpg'

// DATA PENGALAMAN
const experiences = ref([
  {
    period: 'Jan 2026 - Jul 2026',
    title: 'Technical Support',
    company: 'PT. Intersoft Solutions',
    descriptions: [
      'Performed troubleshooting and initial configuration of POS devices',
      'Managed mass import/export data for POS database.',
      'Provided user guidance and training for administrative systems.',
      'Diagnosed and repaired hardware issues, including printers and NFC card readers'
    ],
    imageSrc: isellerImg, // 2. MASUKKAN VARIABEL GAMBAR DI SINI
    imageCaption: 'iSeller POS - 2026'
  },
  {
    period: 'Mei 2025 - Nov 2025',
    title: 'Mobile Developer (Flutter)',
    company: 'PT. Kalanara Group / Strategi Hub Kemenhub',
    descriptions: [
      'Developed responsive mobile application user interfaces using Flutter based on UI/UX designs',
      'Integrated visual components in accordance with design system standards.',
      'Refactored code to improve readability, maintainability, and scalability.',
      'Collaborated with UI/UX designers and stakeholders throughout the development process.'
    ],
    imageSrc: kalanaraImg,
    imageCaption: 'Kalanara - 2025'
  },
  {
    period: 'Jan 2019 - Jan 2025',
    title: 'Warehouse & Store Administrator',
    company: 'PT. Berkahmu Berkahku Muamalah Indonesia',
    descriptions: [
      'Managed employee payroll data, delivery orders, and product listings on e-commerce platforms. ',
      'Coordinated delivery schedules and inventory management.',
      'Handled administrative tasks, including document preparation and data entry.',
      'Coordinated delivery schedules and transportation routes. ',
      'Collaborated with multiple departments to ensure smooth warehouse operations. '
    ],
    imageSrc: gudangImg,
    imageCaption: 'Berkahmu - 2019'
  },
  {
    period: '2020 - 2024',
    title: "Bachelor's Degree in Informatics (Data Science)",
    company: 'Universitas Bhayangkara Jakarta Raya (IPK: 3.62)',
    descriptions: [
      'Skripsi: "A Bi-LSTM Based Model to Identify Key Information from Political News in the 2024 Indonesian Election Event"'
    ],
    imageSrc: unbhayangkaraImg,
    imageCaption: 'Informatics - 2024'
  }
])
</script>