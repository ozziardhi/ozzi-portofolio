<template>
  <section id="about" class="py-20 px-6 max-w-4xl mx-auto">
    <div class="text-center mb-10">
      <h2 class="text-3xl md:text-4xl font-bold font-mono text-purple-400 mb-2">
        // About Me
      </h2>
      <p class="text-gray-400 font-mono text-sm">
        ~ A quick intro about who I am and what I do ~
      </p>
    </div>

    <!-- Kotak Retro Bio -->
    <div class="retro-box bg-[#161b22] p-8 rounded-xl space-y-6 text-gray-300 font-mono text-sm md:text-base leading-relaxed">
      <!-- Loop paragraf dari data terpisah -->
      <p v-for="(paragraph, index) in aboutData.paragraphs" :key="index" v-html="paragraph"></p>

      <div class="border-t border-[#30363d] pt-4 mt-4">
        <p class="text-purple-300 font-bold" v-html="aboutData.callout"></p>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref } from 'vue'

// DATA Teks About (Sangat mudah diedit di sini dalam Bahasa Inggris yang santai/humanoid)
const aboutData = ref({
  paragraphs: [
    "Hi there! I'm <span class='text-purple-400 font-bold'>Ozzi Ardhiyanto</span>, an Informatics graduate from Universitas Bhayangkara Jakarta Raya[cite: 8]. I have a deep passion for mobile app development (especially Flutter), IT support, and smooth operational workflows. I genuinely enjoy building clean, functional apps using modern state management like Clean Architecture, BLoC, and Hive.",
    "Throughout my journey, I've loved blending technical engineering with hands-on operational support—ranging from troubleshooting hardware and organizing sales data to crafting responsive UI layouts for mobile projects. To me, creating systems that just work reliably and smoothly is what makes this field so exciting."
  ],
  callout: "I'm actively open to professional opportunities in IT support, Flutter mobile development, frontend engineering, or administrative roles where I can keep growing and deliver real, meaningful impact!"
})
</script>