<script setup>
import { ref, computed } from "vue";
import NavbarComp from "./components/navbar.vue";
import BookCard from "./components/BookCard.vue";
import AddBookModal from "./components/AddBookModal.vue";
import ProfileModal from "./components/ProfileModal.vue";
import LogoutModal from "./components/LogoutModal.vue";
import Favorite from "./components/Favorite.vue";
import BookDetail from "./components/BookDetail.vue";

// Halaman: 'login', 'forgotPassword', 'discover', 'category', 'favourite'
const currentPage = ref("login");
const showProfileModal = ref(false);
const showLogoutModal = ref(false);
const showAddBookModal = ref(false);
const showMenuFor = ref(null);

const profileName = ref("");
const profileEmail = ref("");
const profileBio = ref("");
const loginEmail = ref("");

const selectedBook = ref(null);
const selectedCategory = ref(null);
const searchQuery = ref("");
const favouriteBooks = ref([]);

const newBook = ref({ title: "", synopsis: "", author: "", category: "romance" });

const categories = [
  { key: "romance", label: "romance", emoji: "🌸" },
  { key: "horror", label: "horror", emoji: "👻" },
  { key: "sejarah", label: "sejarah", emoji: "🌍" },
  { key: "motivasi", label: "berpikir positiv", emoji: "🧠" },
  { key: "pendidikan", label: "pendidikan", emoji: "🎓" },
  { key: "politik", label: "politik", emoji: "🏛️" },
];

const booksByCategory = ref({
  romance: [
    {
      title: "si cinta",
      author: "penulis buku",
      emoji: "🌸",
      synopsis: "Kisah cinta yang indah dan menyentuh hati.",
    },
    {
      title: "bunga hati",
      author: "penulis buku",
      emoji: "💐",
      synopsis: "Perjalanan cinta dua insan yang penuh liku.",
    },
  ],
  horror: [
    {
      title: "pocong mumun",
      author: "penulis buku",
      emoji: "👻",
      synopsis: "Kisah horor yang menegangkan di malam hari.",
    },
    {
      title: "tembok hitam",
      author: "penulis buku",
      emoji: "🏚️",
      synopsis: "Rumah tua yang penuh misteri dan kegelapan.",
    },
  ],
  sejarah: [
    {
      title: "dunia itu bukat",
      author: "penulis buku",
      emoji: "🌍",
      synopsis: "Sejarah peradaban dunia dari masa ke masa.",
    },
  ],
  motivasi: [
    {
      title: "berpikir positiv",
      author: "penulis buku",
      emoji: "🧠",
      synopsis: "Cara berpikir positif untuk kehidupan lebih baik.",
    },
    {
      title: "galaxy",
      author: "penulis buku",
      emoji: "🌌",
      synopsis: "Eksplorasi pikiran yang seluas galaksi.",
    },
  ],
  pendidikan: [
    {
      title: "pendidikan",
      author: "penulis buku",
      emoji: "🎓",
      synopsis: "Pentingnya pendidikan bagi generasi muda.",
    },
  ],
  politik: [
    {
      title: "maps ff",
      author: "penulis buku",
      emoji: "🗺️",
      synopsis: "Politik dalam peta dunia modern.",
    },
  ],
});

// Hanya tampilkan 6 buku di beranda
const allBooks = computed(() => Object.values(booksByCategory.value).flat());
const berandaBooks = computed(() => allBooks.value.slice(0, 6));

const filteredBooks = computed(() => {
  if (!searchQuery.value.trim()) return berandaBooks.value;
  return allBooks.value.filter((b) =>
    b.title.toLowerCase().includes(searchQuery.value.toLowerCase())
  );
});

const isFavourite = (book) => favouriteBooks.value.some((b) => b.title === book.title);

const toggleFavourite = (book) => {
  const idx = favouriteBooks.value.findIndex((b) => b.title === book.title);
  if (idx === -1) favouriteBooks.value.push(book);
  else favouriteBooks.value.splice(idx, 1);
};

const deleteBook = (book) => {
  Object.keys(booksByCategory.value).forEach((cat) => {
    booksByCategory.value[cat] = booksByCategory.value[cat].filter(
      (b) => b.title !== book.title
    );
  });
  if (selectedBook.value?.title === book.title) selectedBook.value = null;
  showMenuFor.value = null;
};

const addBook = () => {
  if (!newBook.value.title) return;
  const emojiMap = {
    romance: "🌸",
    horror: "👻",
    sejarah: "🌍",
    motivasi: "🧠",
    pendidikan: "🎓",
    politik: "🏛️",
  };
  booksByCategory.value[newBook.value.category].push({
    title: newBook.value.title,
    author: newBook.value.author || "penulis buku",
    synopsis: newBook.value.synopsis || "",
    emoji: emojiMap[newBook.value.category] || "📖",
  });
  newBook.value = { title: "", synopsis: "", author: "", category: "romance" };
  showAddBookModal.value = false;
};

const saveProfile = ({ name, email, bio }) => {
  profileName.value = name;
  profileEmail.value = email;
  profileBio.value = bio;
  showProfileModal.value = false;
};
</script>

<template>
  <!-- ===== LOGIN ===== -->
  <div v-if="currentPage === 'login'" class="min-h-screen bg-white flex flex-col">
    <div class="p-6 flex items-center gap-3">
      <span class="text-4xl">📖</span>
      <span class="text-2xl font-black text-slate-800 tracking-widest uppercase"
        >LIBRARY</span
      >
    </div>
    <div class="flex-1 flex flex-col items-center justify-center px-4">
      <h1 class="text-4xl font-black uppercase tracking-widest text-slate-900 mb-1">
        LIBRARY STUDENT
      </h1>
      <p class="text-xl text-gray-500 mb-8" style="font-family: Georgia, serif">
        silahkan login
      </p>
      <div class="flex items-center justify-center gap-12 w-full max-w-4xl">
        <div class="hidden md:block text-9xl opacity-60">🧍‍♀️</div>
        <div
          class="border-4 border-black rounded-3xl p-8 w-full max-w-sm shadow-lg bg-white"
        >
          <div
            class="flex items-center border-2 border-black rounded-xl px-3 py-2 gap-2 mb-4"
          >
            <span>✉️</span>
            <input
              type="email"
              v-model="loginEmail"
              class="flex-1 outline-none text-base bg-transparent"
              placeholder="email"
            />
          </div>
          <div class="flex items-center border-2 border-black rounded-xl px-3 py-2 gap-2">
            <span>🔒</span>
            <input
              type="password"
              placeholder="••••••••"
              class="flex-1 outline-none text-base bg-transparent"
            />
          </div>
          <div class="text-right text-sm text-gray-500 mt-1 mb-6">
            <button @click="currentPage = 'forgotPassword'" class="hover:underline">
              lupa password?
            </button>
          </div>
          <button
            @click="
              profileEmail = loginEmail;
              currentPage = 'discover';
            "
            class="w-full border-2 border-cyan-400 rounded-full py-3 text-xl font-light tracking-widest hover:bg-cyan-50 transition"
            style="font-family: Georgia, serif"
          >
            login
          </button>
        </div>
        <div class="hidden md:block text-9xl opacity-60">🧍‍♂️</div>
      </div>
    </div>
  </div>

  <!-- ===== LUPA PASSWORD ===== -->
  <div
    v-else-if="currentPage === 'forgotPassword'"
    class="min-h-screen bg-white flex flex-col"
  >
    <div class="p-6 flex items-center gap-3">
      <span class="text-4xl">📖</span>
      <span class="text-2xl font-black text-slate-800 tracking-widest uppercase"
        >LIBRARY</span
      >
    </div>
    <div class="flex-1 flex flex-col items-center justify-center px-4">
      <h1 class="text-3xl font-black text-slate-900 mb-8">masukan password baru</h1>
      <div class="flex items-center justify-center gap-12 w-full max-w-4xl">
        <div class="hidden md:block text-9xl opacity-40">📚</div>
        <div
          class="border-4 border-black rounded-3xl p-8 w-full max-w-sm shadow-lg bg-white"
        >
          <div
            class="flex items-center border-2 border-black rounded-xl px-3 py-2 gap-2 mb-4"
          >
            <span>🔒</span>
            <input
              type="password"
              placeholder="••••••••"
              class="flex-1 outline-none text-base bg-transparent"
            />
          </div>
          <div
            class="flex items-center border-2 border-black rounded-xl px-3 py-2 gap-2 mb-8"
          >
            <span>🔒</span>
            <input
              type="password"
              placeholder="masukan password sekali lagi"
              class="flex-1 outline-none text-base bg-transparent text-gray-400"
            />
          </div>
          <button
            @click="currentPage = 'login'"
            class="w-full border-2 border-black rounded-full py-3 text-xl font-light tracking-widest hover:bg-gray-50 transition"
            style="font-family: Georgia, serif"
          >
            masuk
          </button>
        </div>
        <div class="hidden md:block text-9xl opacity-40">📚</div>
      </div>
    </div>
  </div>

  <!-- ===== MAIN APP ===== -->
  <div v-else class="min-h-screen bg-white flex relative">
    <!-- SIDEBAR -->
    <NavbarComp
      :currentPage="currentPage"
      @navigate="
        (p) => {
          currentPage = p;
          selectedCategory = null;
        }
      "
      @addBook="showAddBookModal = true"
      @logout="showLogoutModal = true"
    />

    <!-- KANAN -->
    <div class="flex-1 flex flex-col min-w-0">
      <!-- NAVBAR ATAS -->
      <div class="flex items-center gap-4 px-6 py-4 bg-white border-b border-gray-100">
        <span class="text-2xl">🔍</span>
        <input
          v-model="searchQuery"
          type="text"
          placeholder="cari buku"
          class="bg-gray-200 rounded-full px-5 py-2 text-base outline-none w-64"
        />
        <div class="flex-1"></div>
        <button
          @click="showProfileModal = true"
          class="text-3xl hover:opacity-70 transition"
        >
          👤
        </button>
      </div>

      <!-- KONTEN + DETAIL -->
      <div class="flex flex-1 overflow-hidden">
        <main class="flex-1 bg-gray-200 p-6 overflow-y-auto">
          <!-- DISCOVER -->
          <div
            v-if="currentPage === 'discover'"
            class="grid grid-cols-2 md:grid-cols-3 gap-4"
          >
            <BookCard
              v-for="book in filteredBooks"
              :key="book.title"
              :book="book"
              :isFavourite="isFavourite(book)"
              :showMenu="showMenuFor === book.title"
              @toggleMenu="showMenuFor = showMenuFor === book.title ? null : book.title"
              @closeMenu="showMenuFor = null"
              @favourite="toggleFavourite(book)"
              @delete="deleteBook(book)"
              @select="selectedBook = book"
            />
            <div
              v-if="filteredBooks.length === 0"
              class="col-span-3 text-center text-gray-400 mt-10"
            >
              Buku tidak ditemukan
            </div>
          </div>

          <!-- CATEGORY -->
          <div v-else-if="currentPage === 'category'">
            <div v-if="!selectedCategory" class="grid grid-cols-3 gap-6">
              <div
                v-for="cat in categories"
                :key="cat.key"
                @click="selectedCategory = cat.key"
                class="bg-white rounded-2xl p-6 flex flex-col items-center gap-3 cursor-pointer hover:shadow-md transition"
              >
                <span class="text-7xl">{{ cat.emoji }}</span>
                <span class="font-semibold text-lg">{{ cat.label }}</span>
              </div>
            </div>
            <div v-else>
              <button
                @click="selectedCategory = null"
                class="mb-4 text-blue-600 font-medium"
              >
                ← kembali
              </button>
              <div class="grid grid-cols-2 md:grid-cols-3 gap-4">
                <BookCard
                  v-for="book in booksByCategory[selectedCategory]"
                  :key="book.title"
                  :book="book"
                  :isFavourite="isFavourite(book)"
                  :showMenu="showMenuFor === book.title"
                  @toggleMenu="
                    showMenuFor = showMenuFor === book.title ? null : book.title
                  "
                  @closeMenu="showMenuFor = null"
                  @favourite="toggleFavourite(book)"
                  @delete="deleteBook(book)"
                  @select="selectedBook = book"
                />
              </div>
            </div>
          </div>

          <!-- FAVOURITE -->
          <Favorite
            v-else-if="currentPage === 'favourite'"
            :books="favouriteBooks"
            @select="selectedBook = $event"
            @unfavourite="toggleFavourite($event)"
          />
        </main>

        <!-- BOOK DETAIL panel kanan -->
        <BookDetail :selectedBook="selectedBook" @close="selectedBook = null" />
      </div>
    </div>

    <!-- MODAL PROFIL -->
    <ProfileModal
      v-if="showProfileModal"
      :profileName="profileName"
      :profileEmail="profileEmail"
      :profileBio="profileBio"
      @close="showProfileModal = false"
      @save="saveProfile"
    />

    <!-- MODAL TAMBAH BUKU -->
    <AddBookModal
      v-if="showAddBookModal"
      :newBook="newBook"
      :categories="categories"
      @close="showAddBookModal = false"
      @add="addBook"
    />

    <!-- MODAL LOGOUT -->
    <LogoutModal
      v-if="showLogoutModal"
      @close="showLogoutModal = false"
      @logout="
        () => {
          showLogoutModal = false;
          currentPage = 'login';
        }
      "
    />
  </div>
</template>
