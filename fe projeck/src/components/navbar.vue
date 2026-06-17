<script setup>
defineProps({ currentPage: String });
const emit = defineEmits(["navigate", "addBook", "logout"]);
</script>

<template>
  <aside class="w-56 bg-white border-r border-gray-200 flex flex-col shrink-0">
    <!-- Logo -->
    <div class="flex items-center gap-2 px-5 py-5">
      <span class="text-3xl">📖</span>
      <span class="text-xl font-black tracking-widest uppercase text-slate-900"
        >LIBRARY</span
      >
    </div>
    <div class="border-b border-black mx-3 mb-4"></div>

    <!-- Nav menu -->
    <nav class="flex flex-col gap-1 px-3 flex-1">
      <button
        @click="emit('navigate', 'discover')"
        class="flex items-center gap-3 px-3 py-3 rounded-xl text-left font-medium text-base transition"
        :class="
          currentPage === 'discover'
            ? 'bg-gray-100 font-bold'
            : 'hover:bg-gray-50 text-gray-700'
        "
      >
        <span class="text-2xl">🏠</span> beranda
      </button>

      <button
        @click="emit('navigate', 'category')"
        class="flex items-center gap-3 px-3 py-3 rounded-xl text-left font-medium text-base transition"
        :class="
          currentPage === 'category'
            ? 'bg-gray-100 font-bold'
            : 'hover:bg-gray-50 text-gray-700'
        "
      >
        <span class="text-2xl">🔍</span> category
      </button>

      <button
        @click="emit('navigate', 'favourite')"
        class="flex items-center gap-3 px-3 py-3 rounded-xl text-left font-medium text-base transition"
        :class="
          currentPage === 'favourite'
            ? 'bg-gray-100 font-bold'
            : 'hover:bg-gray-50 text-gray-700'
        "
      >
        <span class="text-2xl">☆</span> favorite
      </button>

      <button
        @click="emit('addBook')"
        class="flex items-center gap-3 px-3 py-3 rounded-xl text-left font-medium text-base hover:bg-gray-50 transition text-gray-700"
      >
        <span
          class="w-7 h-7 bg-black text-white rounded-full flex items-center justify-center text-lg font-black"
          >+</span
        >
        tambah buku
      </button>

      <!-- Ilustrasi buku -->
      <div class="mt-6 flex justify-center">
        <span class="text-7xl opacity-40">📖</span>
      </div>
    </nav>

    <!-- Logout -->
    <button
      @click="emit('logout')"
      class="flex items-center gap-2 px-6 py-5 text-gray-700 hover:text-red-600 font-medium text-base transition"
    >
      log out <span class="text-xl">↪</span>
    </button>
  </aside>
</template>
