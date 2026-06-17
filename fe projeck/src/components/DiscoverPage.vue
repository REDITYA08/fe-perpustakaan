<script setup>
import { ref } from "vue";

// Data kategori & buku langsung jadi satu di sini
const categories = ["Romance", "Sci-Fi", "Horror"];
const books = ref([
  { title: "Cinta Terlarang", category: "Romance" },
  { title: "Masa Depan", category: "Sci-Fi" },
  { title: "Malam Jumat", category: "Horror" },
]);
</script>

<template>
  <div class="space-y-8">
    <!-- List Per Kategori -->
    <div v-for="cat in categories" :key="cat">
      <h2 class="text-xl font-bold mb-4 text-slate-700">{{ cat }}</h2>
      <div class="flex gap-4">
        <div
          v-for="book in books.filter((b) => b.category === cat)"
          :key="book.title"
          class="p-6 bg-slate-100 rounded-xl w-40 h-40 flex items-center justify-center font-semibold"
        >
          {{ book.title }}
        </div>
      </div>
    </div>
  </div>
</template>
