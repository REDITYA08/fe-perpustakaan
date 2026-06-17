<script setup>
defineProps({
  book: Object,
  isFavourite: Boolean,
  showMenu: Boolean,
});
const emit = defineEmits(["toggleMenu", "closeMenu", "favourite", "delete", "select"]);
</script>

<template>
  <div
    class="bg-white rounded-2xl p-3 shadow-sm relative cursor-pointer"
    @click="emit('select', book)"
  >
    <!-- 3 titik menu kiri atas -->
    <div
      class="absolute top-3 left-3 flex flex-col gap-0.5 cursor-pointer z-10"
      @click.stop="emit('toggleMenu')"
    >
      <span class="w-1.5 h-1.5 bg-black rounded-full block"></span>
      <span class="w-1.5 h-1.5 bg-black rounded-full block"></span>
      <span class="w-1.5 h-1.5 bg-black rounded-full block"></span>
    </div>

    <!-- Dropdown hapus buku -->
    <div
      v-if="showMenu"
      class="absolute top-8 left-2 bg-pink-400 text-white rounded-xl px-4 py-2 z-20 shadow-lg text-sm"
      @click.stop
    >
      <div class="font-bold mb-1">hapus buku</div>
      <div class="flex gap-3">
        <button @click="emit('closeMenu')" class="font-medium hover:underline">
          tidak
        </button>
        <button @click="emit('delete')" class="font-bold hover:underline">iya</button>
      </div>
    </div>

    <!-- Tombol favorit kanan atas — putih dulu, merah kalau sudah difavourite -->
    <button
      @click.stop="emit('favourite')"
      class="absolute top-2 right-2 text-2xl z-10 transition-all"
      :class="
        isFavourite ? 'text-red-500' : 'text-white drop-shadow-[0_0_1px_rgba(0,0,0,0.4)]'
      "
    >
      ❤
    </button>

    <!-- Emoji buku -->
    <div class="text-6xl text-center py-6 select-none">{{ book.emoji }}</div>

    <!-- Info -->
    <div class="text-center mt-1">
      <div class="font-semibold text-sm text-gray-800 truncate">{{ book.title }}</div>
      <div class="text-xs text-gray-500">{{ book.author }}</div>
    </div>
  </div>
</template>
