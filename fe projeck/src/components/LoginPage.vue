<template>
  <div class="min-h-screen flex items-center justify-center bg-gray-50 p-4">
    <div
      class="w-full max-w-md bg-white p-8 rounded-3xl shadow-lg border border-gray-100"
    >
      <h1 class="text-center font-bold text-2xl mb-8">LIBRARY</h1>

      <button
        @click="$emit('login-success')"
        class="w-full bg-blue-900 text-white p-3 rounded-xl font-bold"
      >
        LOGIN
      </button>
    </div>
  </div>
</template>

<script setup>
// Ini bagian penting agar error "At least one <script> is required" hilang
defineEmits(["login-success"]);
</script>
