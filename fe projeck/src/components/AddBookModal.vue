<script setup>
defineProps({
  newBook: Object,
  categories: Array,
});
const emit = defineEmits(["close", "add"]);
</script>

<template>
  <div
    class="absolute inset-0 flex items-center justify-center z-50"
    @click.self="emit('close')"
  >
    <div class="bg-pink-400 rounded-3xl p-6 w-96 shadow-2xl text-white">
      <!-- Header -->
      <div class="flex items-center gap-2 mb-4">
        <span
          class="w-8 h-8 bg-black text-white rounded-full flex items-center justify-center text-lg font-black"
          >+</span
        >
        <span class="text-xl font-bold">tambah buku</span>
      </div>

      <!-- Form -->
      <div class="space-y-3">
        <div>
          <div class="text-sm mb-1">judul buku</div>
          <input
            v-model="newBook.title"
            class="w-full bg-white text-gray-800 rounded-lg px-3 py-2 outline-none"
          />
        </div>
        <div>
          <div class="text-sm mb-1">sinopsis buku</div>
          <input
            v-model="newBook.synopsis"
            class="w-full bg-white text-gray-800 rounded-lg px-3 py-2 outline-none"
          />
        </div>
        <div>
          <div class="text-sm mb-1">penulis</div>
          <input
            v-model="newBook.author"
            class="w-full bg-white text-gray-800 rounded-lg px-3 py-2 outline-none"
          />
        </div>
        <div>
          <div class="text-sm mb-1">category</div>
          <div class="relative">
            <select
              v-model="newBook.category"
              class="w-full bg-white text-gray-800 rounded-lg px-3 py-2 outline-none appearance-none"
            >
              <option v-for="cat in categories" :key="cat.key" :value="cat.key">
                {{ cat.label }}
              </option>
            </select>
            <span class="absolute right-3 top-2 text-gray-500 pointer-events-none"
              >↓</span
            >
          </div>
        </div>
      </div>

      <!-- Tombol -->
      <div class="flex justify-between mt-5">
        <button @click="emit('close')" class="font-semibold text-white hover:underline">
          back
        </button>
        <button @click="emit('add')" class="font-bold text-white hover:underline">
          oke
        </button>
      </div>
    </div>
  </div>
</template>
