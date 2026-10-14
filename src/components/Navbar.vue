<template>
  <header class="fixed top-0 left-0 w-full bg-[#0d1117]/80 backdrop-blur border-b border-[#30363d] z-50 px-6 py-4 flex justify-between items-center">
    <!-- Diubah menjadi link yang bisa diklik untuk kembali ke Hero Section (#about) -->
    <a href="#Hero" class="font-mono text-purple-400 font-bold text-sm hover:text-purple-300 transition cursor-pointer flex items-center gap-1">
      <span>~/ozzi-portfolio</span> <span class="animate-pulse">_</span>
    </a>
    <nav class="hidden md:flex gap-6 text-sm font-mono">
      <a href="#about" class="hover:text-purple-400 transition">#about</a>
      <a href="#skills" class="hover:text-purple-400 transition">#skills</a>
      <a href="#projects" class="hover:text-purple-400 transition">#projects</a>
      <a href="#contact" class="hover:text-purple-400 transition">#contact</a>
    </nav>
  </header>
</template>