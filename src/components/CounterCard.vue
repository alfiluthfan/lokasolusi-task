<template>
  <div class="bg-gray-50 rounded-2xl p-6 shadow-sm w-full max-w-md border border-gray-200">
    <header class="mb-4">
      <h2 class="text-lg font-semibold text-gray-800">Counter Sederhana</h2>
      <p class="text-sm text-gray-500">Tombol + / -, nilai tidak boleh kurang dari 0.</p>
    </header>

    <div class="flex items-center justify-between">
      <div class="text-4xl font-extrabold text-gray-900" aria-live="polite">{{ count }}</div>

      <div class="flex gap-3 items-center">
        <button
          @click="decrement"
          :disabled="count === 0"
          aria-label="Kurangi"
          :class="[
            'px-4 py-2 rounded-md border transition-all duration-150',
            count === 0
              ? 'opacity-50 cursor-not-allowed bg-gray-200 text-gray-400 border-gray-200'
              : 'inline-flex items-center justify-center px-4 py-2 rounded-md border bg-gray-200 text-gray-700 hover:bg-gray-300'
          ]"
        >
          -
        </button>

        <button
          @click="increment"
          aria-label="Tambah"
          class="inline-flex items-center justify-center px-4 py-2 rounded-md bg-gray-800 text-white font-medium shadow-sm hover:bg-gray-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-gray-300 transition"
        >
          +
        </button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
const count = ref(0)
function increment() { count.value++ }
function decrement() { if (count.value > 0) count.value-- }
</script>
