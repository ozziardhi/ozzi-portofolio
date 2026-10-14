<template>
  <section id="Hero" class="min-h-screen flex flex-col justify-center items-center text-center px-4 pt-24 relative overflow-hidden">
    
    <!-- Elemen Hiasan Terminal Box Kecil di Sudut (Menambah kesan penuh & retro) -->
    <div class="hidden lg:block absolute top-28 left-16 retro-box bg-[#161b22] p-4 rounded-lg text-left font-mono text-xs text-purple-300 opacity-80 pointer-events-none">
      <div class="flex items-center gap-2 mb-2 border-b border-[#30363d] pb-2">
        <span class="w-2.5 h-2.5 rounded-full bg-red-500 inline-block"></span>
        <span class="w-2.5 h-2.5 rounded-full bg-yellow-500 inline-block"></span>
        <span class="w-2.5 h-2.5 rounded-full bg-green-500 inline-block"></span>
        <span class="text-gray-400 ml-2">system_status.sh</span>
      </div>
      <p class="text-gray-400">&gt; Location: <span class="text-white">Bekasi, ID</span></p>
      <p class="text-gray-400">&gt; Status: <span class="text-green-400">Available for Hire</span></p>
      <p class="text-gray-400">&gt; Core: <span class="text-purple-400">Flutter & Web</span></p>
    </div>

    <!-- Foto Profil Diperbesar & Lebih Jelas -->
    <div class="w-44 h-44 md:w-52 md:h-52 rounded-2xl border-2 border-purple-400 p-2 mb-6 retro-box bg-purple-950/50 overflow-hidden shadow-[0_0_25px_rgba(168,85,247,0.3)]">
      <img 
        :src="profileImage" 
        alt="Ozzi Ardhiyanto" 
        class="w-full h-full object-cover object-[center_15%] rounded-xl transition duration-500"
      />
    </div>
    
    <h1 class="text-4xl md:text-6xl font-bold tracking-tight mb-4">
      Hi. I'm <span class="text-purple-400  decoration-2">Ozzi Ardhiyanto</span>.
    </h1>
    
    <!-- Bagian Teks dengan Efek Ketik -->
    <div class="max-w-xl mx-auto mb-6 px-4 text-center">
      <p class="text-lg md:text-xl text-gray-300 font-mono leading-relaxed inline">
        <span class="text-purple-400 mr-2">&gt;</span>
        <span>{{ displayedText }}</span>
        <span class="animate-pulse bg-purple-400 w-1.5 h-5 ml-1 inline-block align-baseline"></span>
      </p>
    </div>

    <!-- Badge Tech Stack Utama di Hero Section -->
    <div class="flex flex-wrap justify-center gap-2 mb-8">
      <span class="px-3 py-1 bg-[#161b22] border border-purple-500/40 rounded-full font-mono text-xs text-purple-300">#Flutter</span>
      <span class="px-3 py-1 bg-[#161b22] border border-purple-500/40 rounded-full font-mono text-xs text-purple-300">#Dart</span>
      <span class="px-3 py-1 bg-[#161b22] border border-purple-500/40 rounded-full font-mono text-xs text-purple-300">#Vue.js</span>
      <span class="px-3 py-1 bg-[#161b22] border border-purple-500/40 rounded-full font-mono text-xs text-purple-300">#IT Support</span>
    </div>

    <div class="text-purple-400 my-2 text-2xl font-mono">
      ~ ~ ~ &star; ~ ~ ~
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import profileImage from '../assets/profile.jpg'

const fullText = "Software Engineer & IT Specialist | Building Modern Apps with Flutter | Experienced in Technical Support & Administrative Operations"
const displayedText = ref("")
let index = 0
let isDeleting = false

const typeEffect = () => {
  const currentSpeed = isDeleting ? 25 : 55

  if (!isDeleting && index <= fullText.length) {
    displayedText.value = fullText.substring(0, index)
    index++
    
    if (index > fullText.length) {
      setTimeout(() => {
        isDeleting = true
        typeEffect()
      }, 5000)
      return
    }
  } else if (isDeleting && index >= 0) {
    displayedText.value = fullText.substring(0, index)
    index--
    
    if (index < 0) {
      isDeleting = false
      index = 0
      setTimeout(typeEffect, 500)
      return
    }
  }

  setTimeout(typeEffect, currentSpeed)
}

onMounted(() => {
  typeEffect()
})
</script>