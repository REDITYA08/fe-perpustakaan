<script setup>
import { ref } from "vue";

const props = defineProps({
  profileName: String,
  profileEmail: String,
  profileBio: String,
});
const emit = defineEmits(["close", "save"]);

const name = ref(props.profileName);
const email = ref(props.profileEmail);
const bio = ref(props.profileBio);
</script>

<template>
  <div
    class="absolute inset-0 flex items-center justify-center z-50"
    @click.self="emit('close')"
  >
    <div class="bg-pink-400 rounded-3xl p-6 w-80 shadow-2xl text-white">
      <!-- Header profil -->
      <div class="flex items-center gap-3 mb-4">
        <span
          class="text-5xl bg-black text-white rounded-full w-14 h-14 flex items-center justify-center"
          >👤</span
        >
        <div>
          <div class="font-bold text-xl">{{ name }}</div>
          <div class="text-sm text-pink-100">{{ email }}</div>
        </div>
      </div>

      <!-- Nama -->
      <div class="text-sm mb-1">nama lengkap</div>
      <div class="flex items-center gap-2 bg-teal-600 rounded-full px-4 py-2 mb-3">
        <input
          v-model="name"
          class="flex-1 bg-transparent outline-none text-white font-bold"
        />
        <span>⟳</span>
      </div>

      <!-- Email -->
      <div class="text-sm mb-1">email</div>
      <div class="flex items-center gap-2 bg-teal-600 rounded-full px-4 py-2 mb-3">
        <input
          v-model="email"
          type="email"
          class="flex-1 bg-transparent outline-none text-white"
        />
        <span>⟳</span>
      </div>

      <!-- Bio -->
      <div class="text-sm mb-1">biodata singkat</div>
      <div class="flex items-center gap-2 bg-teal-600 rounded-full px-4 py-2 mb-4">
        <input v-model="bio" class="flex-1 bg-transparent outline-none text-white" />
        <span>⟳</span>
      </div>

      <button
        @click="emit('save', { name, email, bio })"
        class="w-full bg-teal-600 rounded-full py-2 font-bold text-white hover:bg-teal-700 transition"
      >
        back
      </button>
    </div>
  </div>
</template>
