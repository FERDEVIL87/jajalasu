<script setup>
import { ref, onMounted } from 'vue'

// Gambar dari folder public
const myPhoto = '/pp.webp'

// Teks berjalan
const roles = ['Frontend Developer', 'UI/UX Enthusiast', 'Web Designer', 'Backend Developer', 'Software Engineer']
const currentTitle = ref('')
let titleIndex = 0
let charIndex = 0
let typingForward = true

function typeWriter() {
  const role = roles[titleIndex]
  if (typingForward) {
    if (charIndex < role.length) {
      currentTitle.value += role.charAt(charIndex)
      charIndex++
    } else {
      typingForward = false
      setTimeout(typeWriter, 1500)
      return
    }
  } else {
    if (charIndex > 0) {
      currentTitle.value = role.substring(0, charIndex - 1)
      charIndex--
    } else {
      typingForward = true
      titleIndex = (titleIndex + 1) % roles.length
    }
  }
  setTimeout(typeWriter, typingForward ? 100 : 50)
}

onMounted(() => {
  typeWriter()
})

function scrollToSection(id) {
  const section = document.getElementById(id)
  if (section) {
    const yOffset = -70
    const y = section.getBoundingClientRect().top + window.scrollY + yOffset
    window.scrollTo({ top: y, behavior: 'smooth' })
  }
}
</script>

<template>
  <section
    id="profil"
    aria-label="Profil Izzuddin Akmal"
    v-intersect
    class="relative overflow-hidden py-24 md:py-32 transition-colors duration-500 bg-gradient-to-br from-white via-blue-50 to-gray-100 dark:from-gray-900 dark:via-gray-800 dark:to-gray-900"
  >
    <!-- SVG Blob -->
    <svg
      class="absolute w-[350px] h-[350px] md:w-[450px] md:h-[450px] -z-10 opacity-20 md:opacity-30 top-1/2 left-1/2 transform -translate-x-1/2 -translate-y-1/2 pointer-events-none"
      viewBox="0 0 200 200"
      xmlns="http://www.w3.org/2000/svg"
    >
      <path
        fill="#3b82f6"
        d="M53.7,-58.6C68.8,-46.5,78.2,-23.3,75.3,-2.4C72.3,18.4,57.1,36.8,42.1,49.5C27.1,62.2,13.5,69.1,-3.7,73.2C-20.9,77.3,-41.8,78.6,-55.6,68.3C-69.4,57.9,-76,36,-74.6,16.2C-73.2,-3.6,-63.7,-21.3,-51.3,-34.6C-39,-47.8,-24,-56.6,-6.5,-61.3C11.1,-65.9,22.2,-66.9,53.7,-58.6Z"
        transform="translate(100 100)"
      />
    </svg>

    <div class="max-w-7xl mx-auto px-6 flex flex-col-reverse md:flex-row items-center gap-12">
      <!-- Text -->
      <div class="md:w-1/2 text-center md:text-left scroll-hidden-left" v-intersect="'animate-fade-in-up'">
        <h1 class="text-4xl sm:text-5xl font-extrabold leading-tight mb-3 bg-gradient-to-r from-blue-600 via-purple-500 to-pink-500 text-transparent bg-clip-text">
          Halo, Saya Izzuddin Akmal
        </h1>

        <p class="text-xl text-gray-500 dark:text-gray-400 mb-2 h-6">
          <span class="font-semibold text-blue-600 dark:text-blue-400">{{ currentTitle }}</span>
          <span class="blinking-cursor">|</span>
        </p>

        <p class="text-lg sm:text-xl text-gray-600 dark:text-gray-300 mb-6">
          Mahasiswa Teknik Informatika yang bersemangat dalam
          <span class="font-semibold text-blue-500 dark:text-blue-300">pengembangan web</span> dan
          <span class="font-semibold text-pink-500 dark:text-pink-400">desain antarmuka</span>.
        </p>

        <!-- Tombol -->
        <div class="flex justify-center md:justify-start gap-4 flex-wrap">
          <button
            @click="scrollToSection('kontak')"
            class="bg-blue-600 dark:bg-blue-500 text-white font-medium py-3 px-6 rounded-xl hover:bg-blue-700 dark:hover:bg-blue-600 transition shadow-md hover:shadow-lg animate-pulse-glow"
          >
            📩 Hubungi Saya
          </button>
          <button
            @click="scrollToSection('proyek')"
            class="border border-blue-600 dark:border-blue-400 text-blue-600 dark:text-blue-300 font-medium py-3 px-6 rounded-xl hover:bg-blue-600 hover:text-white dark:hover:bg-blue-500 dark:hover:text-white transition"
          >
            💼 Lihat Proyek
          </button>
        </div>
      </div>

      <!-- Foto -->
      <div class="md:w-1/2 flex justify-center relative scroll-hidden-right" v-intersect="'animate-fade-in-up'">
        <div class="relative group">
          <img
            :src="myPhoto"
            alt="Foto Profil"
            loading="lazy"
            class="w-52 h-52 sm:w-80 sm:h-80 rounded-full object-cover shadow-xl ring-4 ring-white dark:ring-gray-700
                   transform group-hover:scale-105 transition duration-500 ease-in-out"
            style="object-position: 60% center"
            @error="(e) => e.target.src = '/fallback.webp'"
          />
          <div
            class="absolute inset-0 rounded-full ring-4 ring-blue-400 dark:ring-blue-600 animate-pulse opacity-0
                   group-hover:opacity-100 transition-opacity duration-700"
          ></div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
@keyframes pulse-glow {
  0%, 100% { box-shadow: 0 0 0 0 rgba(59,130,246, 0.6); }
  50% { box-shadow: 0 0 15px 8px rgba(59,130,246, 0.3); }
}
.animate-pulse-glow {
  animation: pulse-glow 2s infinite;
}

@keyframes fade-in-up {
  0% {
    opacity: 0;
    transform: translateY(20px);
  }
  100% {
    opacity: 1;
    transform: translateY(0);
  }
}
.animate-fade-in-up {
  animation: fade-in-up 0.8s ease-out both;
}

.blinking-cursor {
  display: inline-block;
  width: 1px;
  background-color: currentColor;
  animation: blink 1s step-end infinite;
  margin-left: 2px;
  height: 1em;
  vertical-align: bottom;
}
@keyframes blink {
  0%, 100% { opacity: 1 }
  50% { opacity: 0 }
}
</style>
