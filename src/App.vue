<template>
  <div class="min-h-screen bg-primary-50/60 py-12 px-4 sm:px-8">
    <div class="max-w-6xl mx-auto">
      <header class="mb-8 flex flex-col sm:flex-row sm:items-center sm:justify-between gap-4">
        <div>
          <h1 class="text-3xl font-extrabold text-slate-900">Demo Task Lokasoulusi</h1>
          <p class="text-sm text-slate-600 mt-1">Muhammad Alfi Luthfan Thufail</p>
        </div>
      </header>

      <main class="grid gap-6">
        <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
          <CounterCard />
          <NameFormCard />
        </div>

        <TodoListCard />
      </main>
    </div>
  </div>
</template>

<script setup>
import CounterCard from './components/CounterCard.vue'
import NameFormCard from './components/NameFormCard.vue'
import TodoListCard from './components/TodoListCard.vue'
</script>
