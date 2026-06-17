<script setup>
defineProps({ books: Array });
const emit = defineEmits(["select", "unfavourite"]);
</script>

<template>
  <div>
    <div v-if="books.length === 0" class="text-center text-gray-400 mt-10">
      Belum ada buku favorit
    </div>
    <div class="grid grid-cols-2 md:grid-cols-4 gap-4">
      <div
        v-for="book in books"
        :key="book.title"
        class="bg-white rounded-2xl p-3 shadow-sm relative cursor-pointer"
        @click="emit('select', book)"
      >
        <button
          @click.stop="emit('unfavourite', book)"
          class="absolute top-3 right-3 text-xl z-10"
        >
          ❤️
        </button>
        <div class="text-6xl text-center py-6">{{ book.emoji }}</div>
        <div class="text-center mt-1">
          <div class="font-semibold text-sm text-gray-800">{{ book.title }}</div>
          <div class="text-xs text-gray-500">{{ book.author }}</div>
        </div>
      </div>
    </div>
  </div>
</template>
