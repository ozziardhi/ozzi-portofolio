<template>
  <section id="skills" class="py-20 px-6 max-w-4xl mx-auto">
    <h2 class="text-2xl md:text-3xl font-bold mb-8 text-center font-mono">
      // Skills & Tech Stack
    </h2>
    <div class="flex flex-wrap justify-center gap-3">
      <span 
        v-for="skill in skills" 
        :key="skill"
        class="px-4 py-2 bg-[#161b22] border border-purple-500/50 rounded-full font-mono text-sm text-purple-300 retro-box shadow-none hover:shadow-none"
      >
        {{ skill }}
      </span>
    </div>
  </section>
</template>

<script setup>
import { ref } from 'vue'

const skills = ref([
  'Flutter / Dart',
  'Vue.js / Svelte',
  'Go (Echo v5)',
  'Laravel',
  'Clean Architecture',
  'Linux Environment'
])
</script>