<template>
  <section id="projects" class="py-20 bg-gradient-to-br from-gray-100 to-white">
    <div class="container mx-auto px-6">
      <!-- Heading -->
      <h2 class="text-3xl font-extrabold text-center mb-12 text-gray-800 relative">
        My Projects
        <span class="block w-20 h-1 bg-blue-500 mx-auto mt-2 rounded"></span>
      </h2>

      <!-- Projects Grid -->
      <div class="grid sm:grid-cols-2 md:grid-cols-3 gap-8">
        <div class="bg-white rounded-xl shadow-md hover:shadow-xl transition transform hover:-translate-y-1 p-6 text-center">
          <div class="text-4xl mb-4 text-blue-500">🧾</div>
          <h3 class="font-semibold text-xl mb-2 text-gray-800">CRUD Siswa</h3>
          <p class="text-sm text-gray-600">Aplikasi sederhana untuk mengambil data siswa </p>
        </div>

        <div class="bg-white rounded-xl shadow-md hover:shadow-xl transition transform hover:-translate-y-1 p-6 text-center">
          <div class="text-4xl mb-4 text-purple-500">🌐</div>
          <h3 class="font-semibold text-xl mb-2 text-gray-800">Website Portfolio</h3>
          <p class="text-sm text-gray-600">Tampilan personal portfolio dengan Nuxt.js dan Tailwind CSS.</p>
        </div>

        <div class="bg-white rounded-xl shadow-md hover:shadow-xl transition transform hover:-translate-y-1 p-6 text-center">
          <div class="text-4xl mb-4 text-pink-500">🛒</div>
          <h3 class="font-semibold text-xl mb-2 text-gray-800">Toko Online</h3>
          <p class="text-sm text-gray-600">Sistem e-commerce sederhana dengan fitur keranjang & checkout.</p>
        </div>
      </div>
    </div>
  </section>
</template>
