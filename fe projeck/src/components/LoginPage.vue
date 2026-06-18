<template>
  <div class="min-h-screen flex items-center justify-center bg-gray-50 p-4">
    <div
      class="w-full max-w-md bg-white p-8 rounded-3xl shadow-lg border border-gray-100"
    >
      <h1 class="text-center font-bold text-2xl mb-8">LIBRARY</h1>

      <div class="space-y-4">
        <!-- Nama -->
        <div>
          <label class="text-sm font-semibold text-gray-700 block mb-1">Nama</label>
          <input
            v-model="inputName"
            type="text"
            placeholder="Masukkan nama kamu"
            class="w-full border border-gray-200 rounded-xl px-4 py-3 text-sm focus:outline-none focus:border-blue-500 bg-gray-50"
          />
        </div>

        <!-- Email -->
        <div>
          <label class="text-sm font-semibold text-gray-700 block mb-1">Email</label>
          <input
            v-model="inputEmail"
            type="email"
            placeholder="contoh: user@email.com"
            class="w-full border border-gray-200 rounded-xl px-4 py-3 text-sm focus:outline-none focus:border-blue-500 bg-gray-50"
          />
        </div>

        <!-- Password -->
        <div>
          <label class="text-sm font-semibold text-gray-700 block mb-1">Password</label>
          <input
            v-model="inputPassword"
            type="password"
            placeholder="***********"
            class="w-full border border-gray-200 rounded-xl px-4 py-3 text-sm focus:outline-none focus:border-blue-500 bg-gray-50"
          />
        </div>

        <p v-if="errorMsg" class="text-red-500 text-xs">{{ errorMsg }}</p>

        <button
          @click="handleLogin"
          class="w-full bg-blue-900 text-white p-3 rounded-xl font-bold mt-2"
        >
          LOGIN
        </button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";

const emit = defineEmits(["login-success"]);

const inputName = ref("");
const inputEmail = ref("");
const inputPassword = ref("");
const errorMsg = ref("");

function handleLogin() {
  if (!inputName.value || !inputEmail.value || !inputPassword.value) {
    errorMsg.value = "Semua field harus diisi.";
    return;
  }
  errorMsg.value = "";
  emit("login-success", {
    name: inputName.value,
    email: inputEmail.value,
  });
}
</script>
