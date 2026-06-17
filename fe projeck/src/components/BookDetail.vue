<script setup>
defineProps({ selectedBook: Object });
const emit = defineEmits(["close"]);
</script>

<template>
  <aside
    v-if="selectedBook"
    class="w-72 bg-white border-l border-gray-200 p-5 flex flex-col shrink-0 overflow-y-auto"
  >
    <!-- Header -->
    <div class="flex justify-between items-center mb-4">
      <span class="text-xs text-gray-400 font-medium">Detail Buku</span>
      <button
        @click="emit('close')"
        class="text-gray-400 hover:text-black text-xl leading-none"
      >
        ✕
      </button>
    </div>

    <!-- Cover emoji -->
    <div class="text-8xl text-center py-8 bg-gray-100 rounded-2xl mb-4 select-none">
      {{ selectedBook.emoji }}
    </div>

    <!-- Judul & penulis -->
    <div class="text-center mb-4">
      <h3 class="font-bold text-gray-800 text-base">{{ selectedBook.title }}</h3>
      <p class="text-xs text-gray-500 mt-1">{{ selectedBook.author }}</p>
    </div>

    <!-- Sinopsis -->
    <div class="text-xs text-gray-400 font-semibold mb-1 uppercase tracking-wider">
      Sinopsis
    </div>
    <p class="text-sm text-gray-600 leading-relaxed flex-1">
      {{ selectedBook.synopsis || "Tidak ada sinopsis." }}
    </p>

    <!-- Tombol baca -->
    <button
      class="mt-6 w-full bg-gray-200 hover:bg-gray-300 rounded-full py-2 text-sm font-semibold transition"
    >
      baca sekarang
    </button>
  </aside>
</template>
