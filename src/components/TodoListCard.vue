<template>
  <div class="bg-gray-50 rounded-2xl p-6 shadow-sm w-full max-w-xl border border-gray-200">
    <header class="mb-4 flex items-start justify-between">
      <div>
        <h2 class="text-lg font-semibold text-gray-800">Todo List Mini</h2>
      </div>
      <div class="text-sm text-gray-600">
        <span class="font-medium text-gray-800">{{ completedCount }}</span>/<span class="text-gray-600">{{ todos.length }}</span> selesai
      </div>
    </header>

    <form @submit.prevent="addTodo" class="mb-4 grid grid-cols-1 sm:grid-cols-[1fr,auto] gap-3">
      <input
        v-model="newTodo"
        type="text"
        placeholder="Tambahkan todo baru..."
        class="w-full border rounded-md px-3 py-2 focus:outline-none focus:ring-2 focus:ring-gray-300 transition border-gray-200 bg-white text-gray-800"
        aria-label="Todo baru"
      />
      <button
        type="submit"
        class="inline-flex items-center justify-center px-4 py-2 rounded-md bg-gray-800 text-white font-medium shadow-sm hover:bg-gray-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-gray-300 transition"
      >
        Tambah
      </button>
    </form>

    <ul class="space-y-2">
      <li v-for="(t, idx) in todos" :key="t.id" class="flex items-center justify-between gap-3">
        <label class="flex items-center gap-3 w-full cursor-pointer">
          <input
            type="checkbox"
            v-model="t.done"
            @change="saveTodos"
            class="w-4 h-4 accent-gray-800"
            :aria-checked="t.done.toString()"
          />
          <span :class="t.done ? 'line-through text-gray-400' : 'text-gray-900'" class="break-words">{{ t.text }}</span>
        </label>

        <div class="flex gap-2 items-center">
          <button @click="removeTodo(idx)" title="Hapus" class="p-1 rounded hover:bg-gray-100 transition">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-gray-600" fill="none" viewBox="0 0 24 24" stroke="currentColor" aria-hidden="true">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"/>
            </svg>
          </button>
        </div>
      </li>
    </ul>

    <div v-if="todos.length === 0" class="mt-4 text-sm text-gray-500">Belum ada todo. Tambahkan yang pertama!</div>

    <div class="mt-4 pt-4 border-t border-gray-100 flex justify-between items-center">
      <div class="text-sm text-gray-600">{{ completedCount }} selesai dari {{ todos.length }}</div>
      <div class="flex gap-2">
        <button @click="clearCompleted" class="px-3 py-1 border rounded-md text-sm hover:bg-gray-100 transition border-gray-200 text-gray-700">Hapus selesai</button>
        <button @click="clearAll" class="px-3 py-1 border rounded-md text-sm hover:bg-gray-100 transition border-gray-200 text-gray-700">Hapus semua</button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue'

const TODOS_KEY = 'app_todos_v1'
const newTodo = ref('')
const todos = ref([])

function loadTodos() {
  try {
    const raw = localStorage.getItem(TODOS_KEY)
    todos.value = raw ? JSON.parse(raw) : []
  } catch {
    todos.value = []
  }
}

function saveTodos() {
  localStorage.setItem(TODOS_KEY, JSON.stringify(todos.value))
}

function addTodo() {
  const text = newTodo.value.trim()
  if (!text) return
  todos.value.unshift({ id: Date.now(), text, done: false })
  newTodo.value = ''
  saveTodos()
}

function removeTodo(index) {
  todos.value.splice(index, 1)
  saveTodos()
}

function clearCompleted() {
  todos.value = todos.value.filter(t => !t.done)
  saveTodos()
}

function clearAll() {
  todos.value = []
  saveTodos()
}

const completedCount = computed(() => todos.value.filter(t => t.done).length)

onMounted(loadTodos)
</script>
