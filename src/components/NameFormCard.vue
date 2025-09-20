<template>
  <div class="bg-gray-50 rounded-2xl p-6 shadow-sm w-full max-w-md border border-gray-200">
    <header class="mb-4">
      <h2 class="text-lg font-semibold text-gray-800">Form Input Nama</h2>
      <p class="text-sm text-gray-500">Auto capitalize setiap kata. Submit kosong error.</p>
    </header>

    <form @submit.prevent="onSubmit" novalidate>
      <label class="block mb-2 text-sm font-medium text-gray-700" for="name">Nama</label>

      <input
        id="name"
        v-model="name"
        @input="onInput"
        type="text"
        placeholder="contoh: jay idzes"
        class="w-full border rounded-md px-3 py-2 mb-2 focus:outline-none focus:ring-2 focus:ring-gray-300 transition border-gray-200 text-gray-800 bg-white"
        aria-describedby="nameHelp nameError"
      />

      <p id="nameHelp" class="text-xs text-gray-400 mb-3">Huruf pertama tiap kata otomatis jadi kapital.</p>

      <div class="flex gap-3">
        <button
          type="submit"
          class="inline-flex items-center justify-center px-4 py-2 rounded-md bg-gray-800 text-white font-medium shadow-sm hover:bg-gray-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-gray-300 transition"
        >
          Submit
        </button>

        <button
          type="button"
          @click="reset"
          class="inline-flex items-center justify-center px-4 py-2 rounded-md border border-gray-200 text-gray-700 hover:bg-gray-100 transition"
        >
          Reset
        </button>
      </div>

      <p v-if="error" id="nameError" class="mt-3 text-sm text-red-600" role="alert">{{ error }}</p>
    </form>

    <div v-if="submittedName" class="mt-5 pt-4 border-t border-gray-100">
      <h3 class="text-sm text-gray-500 mb-2">Nama terkirim</h3>
      <div class="text-lg font-medium text-gray-900">{{ submittedName }}</div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const name = ref('')
const error = ref('')
const submittedName = ref('')

function titleCase(str) {
  return str
    .split(' ')
    .map((w) => (w ? w.charAt(0).toUpperCase() + w.slice(1).toLowerCase() : ''))
    .join(' ')
}

function onInput(e) {
  name.value = titleCase(e.target.value)
}

function onSubmit() {
  error.value = ''
  if (!name.value.trim()) {
    error.value = 'Nama wajib diisi'
    submittedName.value = ''
    return
  }
  submittedName.value = name.value
}

function reset() {
  name.value = ''
  error.value = ''
  submittedName.value = ''
}
</script>
