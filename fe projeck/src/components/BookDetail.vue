<template>
  <aside class="w-80 bg-slate-950 text-white p-6 flex flex-col justify-between shrink-0">
    <div>
      <span class="text-xs text-gray-400 font-medium tracking-wider block mb-6">
        Selected Category: <span class="text-white font-semibold">Fiction</span>
      </span>
      
      <div class="bg-white text-slate-900 rounded-2xl p-6 aspect-[3/4] flex flex-col justify-between mb-6 shadow-2xl max-w-[200px] mx-auto">
        <div class="border-b border-gray-100 pb-2">
          <h1 class="text-xl font-serif font-bold tracking-tight text-center">Company <br><span class="font-normal italic">of</span> One</h1>
        </div>
        <div class="text-center text-[10px] uppercase tracking-widest text-gray-500 font-medium">Paul Jarvis</div>
      </div>

      <div class="text-center mb-6">
        <h3 class="text-lg font-bold">Company of One</h3>
        <p class="text-xs text-gray-400 mt-1">Paul Jarvis</p>
        
        <div class="flex items-center justify-center gap-1 mt-2 text-amber-400 text-xs">
          <i class="fa-solid fa-star"></i>
          <i class="fa-solid fa-star"></i>
          <i class="fa-solid fa-star"></i>
          <i class="fa-solid fa-star"></i>
          <i class="fa-solid fa-star"></i>
          <span class="text-white font-semibold ml-1 text-sm">4.8</span>
        </div>
      </div>

      <div class="grid grid-cols-3 gap-2 text-center bg-slate-900/60 p-3 rounded-xl border border-slate-800/50 mb-6">
        <div>
          <div class="text-sm font-bold">320</div>
          <div class="text-[10px] text-gray-400 mt-0.5">Pages</div>
        </div>
        <div class="border-x border-slate-800">
          <div class="text-sm font-bold">643</div>
          <div class="text-[10px] text-gray-400 mt-0.5">Ratings</div>
        </div>
        <div>
          <div class="text-sm font-bold">110</div>
          <div class="text-[10px] text-gray-400 mt-0.5">Reviews</div>
        </div>
      </div>

      <p class="text-xs text-gray-400 leading-relaxed line-clamp-4">
        Company of One offers a refreshingly original business strategy that's focused on a commitment to being better instead of bigger. Why? Because staying small provides the freedom to pursue more meaningful pleasures in life.
      </p>
    </div>

    <button class="w-full bg-blue-600 hover:bg-blue-700 text-white font-semibold py-3 px-4 rounded-xl flex items-center justify-center gap-2 transition shadow-lg shadow-blue-600/20 mt-6">
      Read Now <i class="fa-solid fa-book-open text-sm"></i>
    </button>
  </aside>
</template>