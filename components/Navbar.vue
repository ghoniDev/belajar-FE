<template>
  <header class="bg-gradient-to-r from-blue-600 via-purple-600 to-pink-500 text-white fixed top-0 left-0 w-full z-50 shadow-md">
    <div class="container mx-auto px-4 py-4 flex justify-between items-center">
      <!-- Logo -->
      <h1 class="text-2xl font-extrabold tracking-wider">✨ Ghoni<span class="text-yellow-300">Dev</span></h1>

      <!-- Desktop Navigation -->
      <nav class="hidden md:block">
        <ul class="flex space-x-8 text-white font-medium">
          <li>
            <a href="#home" class="hover:text-yellow-300 transition duration-300 ease-in-out transform hover:scale-105">
              Home
            </a>
          </li>
          <li>
            <a href="#about" class="hover:text-yellow-300 transition duration-300 ease-in-out transform hover:scale-105">
              About
            </a>
          </li>
          <li>
            <a href="#projects" class="hover:text-yellow-300 transition duration-300 ease-in-out transform hover:scale-105">
              Projects
            </a>
          </li>
          <li>
            <a href="#contact" class="hover:text-yellow-300 transition duration-300 ease-in-out transform hover:scale-105">
              Contact
            </a>
          </li>
        </ul>
      </nav>

      <!-- Mobile Menu Button -->
      <div class="md:hidden">
        <button @click="toggleMenu" class="text-white focus:outline-none">
          <svg xmlns="http://www.w3.org/2000/svg" class="w-7 h-7" fill="none" viewBox="0 0 24 24"
               stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                  d="M4 6h16M4 12h16M4 18h16"/>
          </svg>
        </button>
      </div>
    </div>

    <!-- Mobile Menu -->
    <div v-if="isOpen" class="md:hidden bg-gradient-to-b from-pink-500 to-purple-600 px-4 pb-4">
      <ul class="flex flex-col space-y-4 text-white font-medium">
        <li><a href="#home" class="hover:text-yellow-300 transition">Home</a></li>
        <li><a href="#about" class="hover:text-yellow-300 transition">About</a></li>
        <li><a href="#projects" class="hover:text-yellow-300 transition">Projects</a></li>
        <li><a href="#contact" class="hover:text-yellow-300 transition">Contact</a></li>
      </ul>
    </div>
  </header>
</template>

<script setup>
import { ref } from 'vue'
const isOpen = ref(false)
const toggleMenu = () => {
  isOpen.value = !isOpen.value
}
</script>
