<script setup>
import { computed } from "vue";
import BookList from "./BookList.vue";
import BookCard from './BookCard.vue'

// PROPS
const props = defineProps({
  selectedCategory: String,
  booksByCategory: Object,
});

// EMIT
const emit = defineEmits(["select-category", "select-book", "toggle-fav"]);

// ambil kategori dari object
const categories = computed(() => Object.keys(props.booksByCategory || {}));
</script>

<template>
  <div class="space-y-6">
    <!-- LIST CATEGORY -->
    <div v-if="!selectedCategory">
      <div class="w-full bg-blue-50 text-blue-700 text-center py-4 rounded-2xl font-bold">
        Browse All Categories
      </div>

      <div class="grid grid-cols-2 md:grid-cols-4 gap-6 mt-6">
        <button
          v-for="category in categories"
          :key="category"
          @click="emit('select-category', category)"
          class="bg-white border border-gray-100 p-8 rounded-3xl hover:shadow-lg transition text-center flex flex-col items-center gap-3"
        >
          <div class="text-4xl">
            {{
              category === "Fiction"
                ? "🧭"
                : category === "Science Fiction"
                ? "🚀"
                : category === "Romance"
                ? "❤️"
                : category === "History"
                ? "🏛️"
                : category === "Biography"
                ? "📚"
                : "📚"
            }}
          </div>

          <span class="font-bold text-sm">
            {{ category }}
          </span>
        </button>
      </div>
    </div>

    <!-- LIST BOOK PER CATEGORY -->
    <div v-else>
      <button
        @click="emit('select-category', null)"
        class="mb-5 text-blue-600 font-semibold"
      >
        ← Kembali
      </button>

      <h2 class="text-xl font-bold mb-5">
        {{ selectedCategory }}
      </h2>

      <div class="grid grid-cols-2 md:grid-cols-4 gap-4">
        <div
          v-for="book in booksByCategory[selectedCategory]"
          :key="book.title"
          @click="emit('select-book', book)"
          class="relative bg-white border p-4 rounded-xl aspect-[3/4] flex flex-col justify-between cursor-pointer"
        >
          <!-- ACTION BUTTON -->
          <div class="absolute top-2 right-2 flex gap-2">
            <!-- LOVE -->
            <button class="text-lg">❤️</button>

            <!-- 3 DOT -->
            <button class="text-lg">⋮</button>
          </div>

          <!-- BOOK TITLE -->
          <div class="bg-blue-50 p-4 rounded-xl text-center font-bold">
            {{ book.title }}
          </div>

          <p class="text-sm text-gray-500">
            {{ book.author }}
          </p>
        </div>
      </div>
    </div>
  </div>
</template>
