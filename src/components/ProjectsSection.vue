<template>
  <section id="projects" class="py-20 px-6 max-w-6xl mx-auto">
    <div class="text-center mb-16">
      <h2 class="text-3xl md:text-4xl font-bold font-mono text-purple-400 mb-2">
        // Featured Projects
      </h2>
      <p class="text-gray-400 font-mono text-sm">
        ~ Real-world applications & personal masterpieces ~
      </p>
    </div>

    <!-- Grid Projects (Hanya 2 Proyek) -->
    <div class="grid grid-cols-1 md:grid-cols-2 gap-8">
      <div 
        v-for="(project, index) in projects" 
        :key="index"
        class="retro-box bg-[#161b22] p-6 rounded-lg flex flex-col justify-between"
      >
        <div>
          <!-- Thumbnail Utama dengan Efek Kartu Bertumpuk Portrait -->
          <div 
            class="w-full h-64 bg-purple-950/40 rounded border border-purple-500/30 mb-4 overflow-hidden relative group cursor-pointer flex items-center justify-center p-4"
            @click="openModal(project)"
          >
            <!-- Jika project memiliki multi-gambar, buat efek tumpukan kartu portrait -->
            <template v-if="project.images.length > 1 && project.images[0].src">
              <div class="relative w-32 h-48 transition-all duration-500 group-hover:scale-105 group-hover:rotate-1">
                
                <!-- Kartu ke-3 (Paling Belakang / Kanan) -->
                <div v-if="project.images[2]" class="absolute inset-0 bg-[#161b22] rounded-lg border border-purple-500/40 shadow-xl transform rotate-12 translate-x-5 translate-y-2 opacity-70 overflow-hidden">
                  <img :src="project.images[2].src" class="w-full h-full object-cover filter brightness-75" />
                </div>

                <!-- Kartu ke-2 (Tengah / Kiri) -->
                <div v-if="project.images[1]" class="absolute inset-0 bg-[#161b22] rounded-lg border border-purple-500/40 shadow-xl transform -rotate-12 -translate-x-5 translate-y-1 opacity-85 overflow-hidden">
                  <img :src="project.images[1].src" class="w-full h-full object-cover filter brightness-90" />
                </div>

                <!-- Kartu ke-1 (Paling Depan / Utama) -->
                <div class="absolute inset-0 bg-[#161b22] rounded-lg border-2 border-purple-400 shadow-2xl transform rotate-0 overflow-hidden">
                  <img :src="project.images[0].src" class="w-full h-full object-cover" />
                </div>

              </div>
            </template>

            <!-- Fallback jika hanya ada 1 gambar -->
            <template v-else>
              <img 
                v-if="project.images[0] && project.images[0].src" 
                :src="project.images[0].src" 
                :alt="project.title"
                class="w-full h-full object-cover group-hover:scale-105 transition duration-500 rounded"
              />
              <span v-else class="text-purple-300 font-mono text-sm">
                📸 Klik untuk Lihat Detail ({{ project.images.length }} Foto)
              </span>
            </template>
            
            <!-- Overlay Info saat Hover -->
            <div class="absolute inset-0 bg-black/60 opacity-0 group-hover:opacity-100 transition duration-300 flex items-center justify-center z-20">
              <span class="text-purple-300 font-mono text-xs font-bold border border-purple-400 px-3 py-2 rounded bg-[#0d1117]/90 shadow-lg">
                🔍 Click to View Gallery & Details
              </span>
            </div>
          </div>

          <h3 class="font-bold text-2xl text-purple-400 mb-2">{{ project.title }}</h3>
          <p class="text-gray-300 text-sm mb-4 leading-relaxed">{{ project.description }}</p>
        </div>

        <div>
          <!-- Tech Stack Badges -->
          <div class="flex flex-wrap gap-2 mb-6">
            <span 
              v-for="tag in project.tags" 
              :key="tag.name"
              class="px-2.5 py-1 bg-[#0d1117] border border-purple-500/40 rounded text-xs font-mono text-purple-300"
            >
              {{ tag.name }}
            </span>
          </div>

          <!-- Tombol Detail / Galeri -->
          <button 
            @click="openModal(project)"
            class="w-full py-2.5 bg-purple-600 hover:bg-purple-500 text-white font-mono text-sm font-bold rounded transition retro-box shadow-none hover:shadow-none cursor-pointer"
          >
            View Project Details &rarr;
          </button>
        </div>
      </div>
    </div>

    <!-- Modal Pop-up Detail Lengkap -->
    <div v-if="selectedProject" class="fixed inset-0 z-50 bg-black/80 backdrop-blur-sm flex items-center justify-center p-4">
      <div class="retro-box bg-[#161b22] max-w-3xl w-full max-h-[90vh] overflow-y-auto p-6 md:p-8 rounded-xl relative">
        <!-- Tombol Close -->
        <button 
          @click="closeModal"
          class="absolute top-4 right-4 text-gray-400 hover:text-white font-mono text-xl font-bold px-2.5 py-1 rounded border border-gray-600 hover:border-purple-400 cursor-pointer z-10"
        >
          &times;
        </button>

        <h3 class="text-2xl md:text-3xl font-bold text-purple-400 font-mono mb-1">{{ selectedProject.title }}</h3>
        <p class="text-gray-400 text-sm mb-6 font-mono">{{ selectedProject.subtitle }}</p>

        <!-- 1. GAMBAR DI ATAS: Carousel / Slider Ukuran Standar + Fitur Klik untuk Zoom -->
        <div class="mb-8">
          <div class="flex justify-between items-center mb-3">
            <h4 class="text-sm font-mono text-purple-300 font-bold">// Project Screenshots & Preview</h4>
            <span class="text-xs font-mono text-gray-400">(Klik gambar untuk Zoom)</span>
          </div>
          
          <div class="relative w-full h-72 md:h-80 bg-purple-950/60 rounded-lg border border-purple-500/40 overflow-hidden flex flex-col items-center justify-center p-2">
            <!-- Tampilan Foto Aktif (Bisa diklik untuk memperbesar) -->
            <div class="w-full h-full flex flex-col items-center justify-center relative group cursor-zoom-in" @click="zoomImage(selectedProject.images[currentImageIndex])">
              <img 
                v-if="selectedProject.images[currentImageIndex].src" 
                :src="selectedProject.images[currentImageIndex].src" 
                :alt="selectedProject.images[currentImageIndex].caption"
                class="w-full h-full object-contain rounded transition duration-300 group-hover:scale-102"
              />
              <div v-else class="flex flex-col items-center justify-center h-full">
                <span class="text-4xl mb-2">🖼️</span>
                <span class="text-sm font-mono text-purple-200 font-bold">{{ selectedProject.images[currentImageIndex].caption }}</span>
              </div>
              
              <!-- Caption -->
              <span class="absolute bottom-2 bg-black/70 px-3 py-1 rounded text-xs font-mono text-purple-200 backdrop-blur-sm pointer-events-none">
                {{ selectedProject.images[currentImageIndex].caption }} (Slide {{ currentImageIndex + 1 }} dari {{ selectedProject.images.length }})
              </span>
            </div>

            <!-- Tombol Navigasi Carousel (Prev & Next) -->
            <button 
              @click="prevImage" 
              class="absolute left-3 top-1/2 -translate-y-1/2 bg-[#0d1117]/80 hover:bg-purple-600 text-purple-300 hover:text-white px-3 py-2 rounded border border-purple-500/40 font-mono font-bold transition cursor-pointer z-10"
            >
              &larr;
            </button>
            <button 
              @click="nextImage" 
              class="absolute right-3 top-1/2 -translate-y-1/2 bg-[#0d1117]/80 hover:bg-purple-600 text-purple-300 hover:text-white px-3 py-2 rounded border border-purple-500/40 font-mono font-bold transition cursor-pointer z-10"
            >
              &rarr;
            </button>
          </div>

          <!-- Dot Indikator Carousel -->
          <div class="flex justify-center gap-2 mt-3">
            <button 
              v-for="(_, imgIdx) in selectedProject.images" 
              :key="imgIdx"
              @click="currentImageIndex = imgIdx"
              class="w-3 h-3 rounded-full transition cursor-pointer"
              :class="currentImageIndex === imgIdx ? 'bg-purple-500 scale-110' : 'bg-gray-600 hover:bg-gray-500'"
            ></button>
          </div>
        </div>

        <!-- 2. Objective / Tujuan Pembuatan Aplikasi -->
        <div class="mb-6 bg-[#0d1117] p-4 rounded-lg border border-purple-500/30">
          <h4 class="text-sm font-mono text-purple-300 mb-2 font-bold">// Project Objective</h4>
          <p class="text-gray-300 text-sm leading-relaxed">{{ selectedProject.objective }}</p>
        </div>

        <!-- 3. Deskripsi Lengkap -->
        <div class="mb-6">
          <h4 class="text-sm font-mono text-purple-300 mb-2 font-bold">// Detailed Description</h4>
          <p class="text-gray-300 text-sm leading-relaxed whitespace-pre-line">{{ selectedProject.fullDescription }}</p>
        </div>

        <!-- 4. Tech Stack & Fungsinya -->
        <div class="mb-4">
          <h4 class="text-sm font-mono text-purple-300 mb-3 font-bold">// Tech Stack & Functions</h4>
          <div class="grid grid-cols-1 sm:grid-cols-2 gap-3">
            <div 
              v-for="tag in selectedProject.tags" 
              :key="tag.name"
              class="bg-[#0d1117] p-3 rounded border border-purple-500/30"
            >
              <span class="text-purple-400 font-mono font-bold text-xs block mb-1">{{ tag.name }}</span>
              <span class="text-gray-400 font-mono text-xs">{{ tag.function }}</span>
            </div>
          </div>
        </div>

      </div>
    </div>

    <!-- Sub-Modal untuk Zoom Foto Layar Penuh -->
    <div v-if="zoomedImage" class="fixed inset-0 z-60 bg-black/95 backdrop-blur-md flex items-center justify-center p-4" @click="closeZoom">
      <div class="relative max-w-5xl max-h-[95vh] flex flex-col items-center">
        <button 
          @click="closeZoom"
          class="absolute -top-12 right-0 text-gray-300 hover:text-white font-mono text-2xl font-bold px-3 py-1 rounded border border-gray-500 hover:border-purple-400 cursor-pointer"
        >
          &times; Close Zoom
        </button>
        <img :src="zoomedImage.src" :alt="zoomedImage.caption" class="max-w-full max-h-[85vh] object-contain rounded-lg border border-purple-500/50 shadow-2xl" />
        <p class="text-purple-300 font-mono text-sm mt-4 font-bold">{{ zoomedImage.caption }}</p>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref } from 'vue'

// Import gambar Warungku POS
import mainmenuImg from '../assets/warungku/mainmenu.jpg'
import menuImg from '../assets/warungku/menu.jpg'
import databarangImg from '../assets/warungku/databarang.jpg'
import laporanImg from '../assets/warungku/laporan.jpg'
import pengaturanImg from '../assets/warungku/pengaturan.jpg'

// Import gambar Catat Keuangan OCR
import utamaKeuanganImg from '../assets/keuangan/utama.jpg'
import tambaheditKeuanganImg from '../assets/keuangan/tambahedit.jpg'
import laporanKeuanganImg from '../assets/keuangan/laporan.jpg'

const selectedProject = ref(null)
const currentImageIndex = ref(0)
const zoomedImage = ref(null)

const openModal = (project) => {
  selectedProject.value = project
  currentImageIndex.value = 0
}

const closeModal = () => {
  selectedProject.value = null
}

const nextImage = () => {
  if (selectedProject.value) {
    currentImageIndex.value = (currentImageIndex.value + 1) % selectedProject.value.images.length
  }
}

const prevImage = () => {
  if (selectedProject.value) {
    currentImageIndex.value = (currentImageIndex.value - 1 + selectedProject.value.images.length) % selectedProject.value.images.length
  }
}

const zoomImage = (imageObj) => {
  if (imageObj && imageObj.src) {
    zoomedImage.value = imageObj
  }
}

const closeZoom = () => {
  zoomedImage.value = null
}

// DATA PROYEK (Hanya Warungku POS & Catat Keuangan OCR)
const projects = ref([
  {
    title: 'Warungku POS',
    subtitle: 'Point-of-Sale Mobile Application',
    description: 'Aplikasi point-of-sale mobile menggunakan Flutter, Hive, dan Cubit untuk manajemen kasir toko secara offline-first.',
    objective: 'To provide local MSMEs (UMKM) with a fast, lightweight, and reliable offline-first mobile cashier system that simplifies daily transactions and inventory tracking without relying heavily on stable internet connectivity.',
    fullDescription: 'Warungku is custom-built to help store owners manage daily cashier transactions smoothly. Featuring high-speed local data persistence via Hive database and reactive state management using Cubit, the application ensures seamless performance even in offline environments.',
    tags: [
      { name: '#Flutter', function: 'Cross-platform mobile UI framework.' },
      { name: '#Dart', function: 'Primary programming language.' },
      { name: '#Hive', function: 'Ultra-fast NoSQL local database for offline storage.' },
      { name: '#Cubit', function: 'Predictable and lightweight state management pattern.' },
      { name: '#Clean Architecture', function: 'Ensuring modularity, testability, and separation of concerns.' }
    ],
    images: [
      { src: mainmenuImg, caption: 'Main Menu' },
      { src: menuImg, caption: 'Menu Kasir' },
      { src: databarangImg, caption: 'Data Barang' },
      { src: laporanImg, caption: 'Laporan Penjualan' },
      { src: pengaturanImg, caption: 'Pengaturan Sistem' }
    ]
  },
  {
    title: 'Catat Keuangan OCR',
    subtitle: 'Financial Management & Receipt Scanner',
    description: 'Aplikasi manajemen keuangan dengan fitur pemindaian struk otomatis berbasis Google ML Kit OCR.',
    objective: 'To automate daily expense logging and budget tracking by leveraging OCR technology, saving users from manual typing while offering quick PDF reporting features.',
    fullDescription: 'A comprehensive personal finance tracker integrated with Google ML Kit Text Recognition. Users can instantly scan physical receipts to extract transaction details automatically. It also supports local offline storage and dynamic PDF report generation.',
    tags: [
      { name: '#Flutter', function: 'Cross-platform app development.' },
      { name: '#Google ML Kit', function: 'On-device text recognition OCR for scanning receipts.' },
      { name: '#Riverpod', function: 'Robust and type-safe state management.' },
      { name: '#PDF Export', function: 'Generating downloadable financial report documents.' },
      { name: '#Hive', function: 'Lightweight local database for transaction history.' }
    ],
    images: [
      { src: utamaKeuanganImg, caption: 'Halaman Utama' },
      { src: tambaheditKeuanganImg, caption: 'Tambah & Edit Transaksi' },
      { src: laporanKeuanganImg, caption: 'Laporan Keuangan' }
    ]
  }
])
</script>