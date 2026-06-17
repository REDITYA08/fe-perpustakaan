<script setup>
defineProps({
  books: Array,
});

const emit = defineEmits(["select"]);
</script>

<template>
  <div class="grid grid-cols-2 md:grid-cols-4 gap-4">
    <div
      v-for="(book, index) in books"
      :key="index"
      @click="emit('select', book)"
      class="bg-white border border-gray-100 p-3 rounded-2xl hover:shadow-md transition cursor-pointer"
    >
      <div
        class="bg-blue-50 rounded-xl p-4 aspect-[3/4] flex items-center justify-center text-center font-bold text-xs mb-3"
      >
        {{ book.title }}
      </div>

      <h3 class="font-bold text-sm text-gray-800 truncate">
        {{ book.title }}
      </h3>

      <p class="text-xs text-gray-400">
        {{ book.author }}
      </p>
    </div>
  </div>
</template>
