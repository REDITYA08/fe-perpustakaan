<script setup>
defineProps({
  book: Object
})
</script>

<template>
  <div class="w-80 bg-slate-950 text-white p-6 flex flex-col border-l border-slate-900">
    <span class="text-xs text-slate-400 mb-6 block font-medium">Selected Book Detail</span>
    
    <div v-if="book" class="flex flex-col flex-1">
      <div class="bg-white text-slate-900 rounded-2xl p-8 aspect-[3/4] flex flex-col justify-between items-center text-center shadow-xl mb-6">
        <h1 class="text-xl font-extrabold mt-4">{{ book.title }}</h1>
        <span class="text-xs font-bold text-slate-400 tracking-wider uppercase">{{ book.author }}</span>
      </div>

      <h3 class="text-lg font-bold text-center mb-1">{{ book.title }}</h3>
      <p class="text-xs text-slate-400 text-center mb-4">{{ book.author }}</p>
      
      <div class="grid grid-cols-3 gap-2 bg-slate-900 p-3 rounded-xl text-center text-xs mb-4">
        <div><b class="block text-white text-sm">{{ book.pages || '-' }}</b> Pages</div>
        <div><b class="block text-white text-sm">{{ book.ratings || '-' }}</b> Ratings</div>
        <div><b class="block text-white text-sm">{{ book.reviews || '-' }}</b> Reviews</div>
      </div>
      <p class="text-xs text-slate-400 leading-relaxed">{{ book.desc || 'No description available.' }}</p>
    </div>

    <div v-else class="flex-1 flex items-center justify-center text-center text-slate-500 border-2 border-dashed border-slate-800 rounded-2xl p-4">
      <span>👉 Silakan klik salah satu buku untuk melihat detail di sini.</span>
    </div>
  </div>
</template>