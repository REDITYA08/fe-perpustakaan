<script setup>
const emit = defineEmits(["close", "logout"]);
</script>

<template>
  <div
    class="absolute inset-0 flex items-center justify-center z-50"
    @click.self="emit('close')"
  >
    <div class="bg-white rounded-2xl px-8 py-6 shadow-2xl text-center w-80">
      <div class="text-xl font-bold mb-1 flex items-center justify-center gap-2">
        log out <span>↪</span>
      </div>
      <div class="border-t border-gray-300 my-3"></div>
      <div class="flex justify-center gap-12 mt-2">
        <button
          @click="emit('close')"
          class="text-lg font-medium text-gray-700 hover:underline"
        >
          tidak
        </button>
        <button
          @click="emit('logout')"
          class="text-lg font-bold text-gray-900 hover:underline"
        >
          iya
        </button>
      </div>
    </div>
  </div>
</template>
