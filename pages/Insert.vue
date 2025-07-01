<template>
  <div>
    <NavSiswa />

    <!-- Kontainer Konten -->
    <div class="pt-24 px-4 md:px-0 max-w-5xl mx-auto">
      <h1 class="text-3xl font-extrabold mb-6 text-center text-gray-800">📄 Manajemen Data Siswa</h1>

      <!-- Form Card -->
      <div class="bg-white rounded-xl shadow-lg p-6 mb-10 border border-gray-200">
        <h2 class="text-xl font-bold mb-4 text-gray-700">{{ isEdit ? 'Edit Siswa' : 'Tambah Siswa' }}</h2>

        <form @submit.prevent="submitForm" class="grid grid-cols-1 md:grid-cols-2 gap-4">
          <input v-model="form.nisn" type="number" placeholder="NISN" class="input" required />
          <input v-model="form.nama" type="text" placeholder="Nama" class="input" required />
          <input v-model="form.kelas" type="text" placeholder="Kelas" class="input" required />
          <input v-model="form.alamat" type="text" placeholder="Alamat" class="input" required />
          <input v-model="form.tgl_lahir" type="date" class="input" required />
          <select v-model="form.jk" class="input" required>
            <option disabled value="">Jenis Kelamin</option>
            <option value="L">Laki-laki</option>
            <option value="P">Perempuan</option>
          </select>
          <div class="md:col-span-2 flex justify-between mt-2">
            <button type="submit" class="bg-blue-600 text-white px-5 py-2 rounded hover:bg-blue-700 transition">
              {{ isEdit ? 'Update Siswa' : 'Simpan' }}
            </button>
            <button v-if="isEdit" @click="cancelEdit" type="button" class="text-gray-500 hover:text-black underline">
              Batal Edit
            </button>
          </div>
        </form>
      </div>

      <!-- Table Card -->
      <div class="bg-white rounded-xl shadow-lg p-6 border border-gray-200">
        <h2 class="text-xl font-bold mb-4 text-gray-700">📋 Daftar Siswa</h2>
        <div class="overflow-x-auto">
          <table class="w-full text-sm border">
            <thead class="bg-blue-100 text-blue-700">
              <tr>
                <th class="border px-3 py-2 text-left">No</th>
                <th class="border px-3 py-2 text-left">NISN</th>
                <th class="border px-3 py-2 text-left">Nama</th>
                <th class="border px-3 py-2 text-left">Kelas</th>
                <th class="border px-3 py-2 text-left">Alamat</th>
                <th class="border px-3 py-2 text-left">Tgl Lahir</th>
                <th class="border px-3 py-2 text-left">JK</th>
                <th class="border px-3 py-2 text-center">Aksi</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="(siswa, index) in siswaList" :key="siswa.id" class="hover:bg-gray-50 transition">
                <td class="border px-3 py-2">{{ index + 1 }}</td>
                <td class="border px-3 py-2">{{ siswa.nisn }}</td>
                <td class="border px-3 py-2">{{ siswa.nama }}</td>
                <td class="border px-3 py-2">{{ siswa.kelas }}</td>
                <td class="border px-3 py-2">{{ siswa.alamat }}</td>
                <td class="border px-3 py-2">{{ siswa.tgl_lahir }}</td>
                <td class="border px-3 py-2">{{ siswa.jk }}</td>
                <td class="border px-3 py-2 text-center space-x-2">
                  <button @click="editSiswa(siswa)" class="text-blue-600 hover:underline">Edit</button>
                  <button @click="hapusSiswa(siswa.id)" class="text-red-500 hover:underline">Hapus</button>
                </td>
              </tr>
              <tr v-if="siswaList.length === 0">
                <td colspan="8" class="text-center text-gray-500 py-4">Belum ada data siswa.</td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import Navbar from '~/components/Navbar.vue'
import { ref, reactive } from 'vue'

const form = reactive({
  id: null,
  nisn: '',
  nama: '',
  kelas: '',
  alamat: '',
  tgl_lahir: '',
  jk: ''
})

const isEdit = ref(false)
const siswaList = ref([])

const getSiswa = async () => {
  siswaList.value = await $fetch('http://localhost:8000/api/siswa')
}
await getSiswa()

const resetForm = () => {
  Object.assign(form, {
    id: null,
    nisn: '',
    nama: '',
    kelas: '',
    alamat: '',
    tgl_lahir: '',
    jk: ''
  })
  isEdit.value = false
}

const submitForm = async () => {
  if (isEdit.value) {
    await $fetch(`http://localhost:8000/api/siswa/${form.id}`, {
      method: 'PUT',
      body: { ...form }
    })
  } else {
    await $fetch('http://localhost:8000/api/siswa', {
      method: 'POST',
      body: { ...form }
    })
  }
  await getSiswa()
  resetForm()
}

const editSiswa = (siswa) => {
  Object.assign(form, siswa)
  isEdit.value = true
}

const cancelEdit = () => {
  resetForm()
}

const hapusSiswa = async (id) => {
  if (confirm('Yakin ingin menghapus data ini?')) {
    await $fetch(`http://localhost:8000/api/siswa/${id}`, {
      method: 'DELETE'
    })
    await getSiswa()
  }
}

import NavSiswa from '@/components/NavSiswa.vue'
</script>

<style scoped>
.input {
  @apply w-full border rounded px-3 py-2 focus:outline-none focus:ring-2 focus:ring-blue-500;
}
</style>
