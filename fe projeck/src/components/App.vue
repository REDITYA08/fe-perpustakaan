<script setup>
import { ref, computed } from "vue";

// State Navigasi Halaman
const currentPage = ref("discover"); // Pilihan: 'login', 'discover', 'category', 'library', 'favourite'

// State Modal Pop-up
const showProfileModal = ref(false);
const showLogoutModal = ref(false);

// State Data Profil
const profileName = ref("Username");
const profileEmail = ref(" profileEmail ");
const profileBio = ref("Siswa XI PPLG 2 yang suka membaca buku teknologi dan desain.");

// State Buku yang Dipilih
const selectedBook = ref(null);

// State Kategori yang Sedang Dipilih
const selectedCategory = ref(null);

// Search Buku
const searchQuery = ref("");
const favouriteBooks = ref([]);

const showAddBookModal = ref(false);

const newBook = ref({
  title: "",
  author: "",
  category: "Fiction",
});

// Data Dummy Buku Berdasarkan Kategori
const booksByCategory = ref({
  Fiction: [
    {
      title: "The Psychology of Money",
      author: "Morgan Housel",
      rating: "4.9",
      pages: "250",
      ratingsCount: "1.2k",
      reviewsCount: "450",
      desc: "Timeless lessons on wealth, greed, and happiness.",
    },
    {
      title: "Stupore E Tremori",
      author: "Amélie Nothomb",
      rating: "4.5",
      pages: "180",
      ratingsCount: "310",
      reviewsCount: "65",
      desc:
        "A humorous yet biting semi-autobiographical novel about a Western woman navigating corporate Japan.",
    },
    {
      title: "The Great Gatsby",
      author: "F. Scott Fitzgerald",
      rating: "4.4",
      pages: "180",
      ratingsCount: "3.1k",
      reviewsCount: "1.2k",
      desc:
        "The story of the fabulously wealthy Jay Gatsby and his love for the beautiful Daisy Buchanan.",
    },
    {
      title: "To Kill a Mockingbird",
      author: "Harper Lee",
      rating: "4.8",
      pages: "281",
      ratingsCount: "4.5k",
      reviewsCount: "2.1k",
      desc: "A novel about the crisis of conscience and racism in a small Southern town.",
    },
    {
      title: "1984",
      author: "George Orwell",
      rating: "4.7",
      pages: "328",
      ratingsCount: "5.2k",
      reviewsCount: "2.8k",
      desc:
        "A dystopian social science fiction novel and cautionary tale about totalitarianism.",
    },
  ],
  "Non-Fiction": [
    {
      title: "HOW INNOVATION WORKS",
      author: "Matt Ridley",
      rating: "4.7",
      pages: "300",
      ratingsCount: "520",
      reviewsCount: "98",
      desc:
        "Innovation is the main event of the modern age, the reason we experience compounding progress.",
    },
    {
      title: "Company of One",
      author: "Paul Jarvis",
      rating: "4.8",
      pages: "320",
      ratingsCount: "643",
      reviewsCount: "110",
      desc:
        "Company of One offers a refreshingly original business strategy that focused on being better instead of bigger.",
    },
    {
      title: "Sapiens",
      author: "Yuval Noah Harari",
      rating: "4.8",
      pages: "512",
      ratingsCount: "4.3k",
      reviewsCount: "1.9k",
      desc: "A brief history of humankind from ancient times to the modern era.",
    },
    {
      title: "Educated",
      author: "Tara Westover",
      rating: "4.7",
      pages: "352",
      ratingsCount: "2.1k",
      reviewsCount: "940",
      desc:
        "An unforgettable memoir about a young girl who leaves her survivalist family to go to college.",
    },
    {
      title: "Thinking, Fast and Slow",
      author: "Daniel Kahneman",
      rating: "4.6",
      pages: "499",
      ratingsCount: "3.4k",
      reviewsCount: "1.1k",
      desc: "A detailed analysis of the two systems that drive the way we think.",
    },
  ],
  "Science Fiction": [
    {
      title: "PROJECT HAIL MARY",
      author: "Andy Weir",
      rating: "4.9",
      pages: "450",
      ratingsCount: "2.5k",
      reviewsCount: "890",
      desc: "A lone astronaut must save the earth from an extinction-level event.",
    },
    {
      title: "Dune",
      author: "Frank Herbert",
      rating: "4.6",
      pages: "617",
      ratingsCount: "4.1k",
      reviewsCount: "1.8k",
      desc: "Set in the far future amidst a sprawling feudal interstellar empire.",
    },
    {
      title: "The Martian",
      author: "Andy Weir",
      rating: "4.7",
      pages: "369",
      ratingsCount: "3.9k",
      reviewsCount: "1.4k",
      desc:
        "An astronaut becomes stranded on Mars and must use his ingenuity to survive.",
    },
    {
      title: "Neuromancer",
      author: "William Gibson",
      rating: "4.3",
      pages: "271",
      ratingsCount: "1.1k",
      reviewsCount: "430",
      desc: "The matrix is a world within a world, a consensus hallucination.",
    },
  ],
  Fantasy: [
    {
      title: "The Hobbit",
      author: "J.R.R. Tolkien",
      rating: "4.8",
      pages: "310",
      ratingsCount: "5.1k",
      reviewsCount: "2.1k",
      desc: "Bilbo Baggins is whisked away into a breathtaking treasure hunt.",
    },
    {
      title: "Harry Potter",
      author: "J.K. Rowling",
      rating: "4.9",
      pages: "309",
      ratingsCount: "9.2k",
      reviewsCount: "4.5k",
      desc: "The story of a young wizard and his adventures at school.",
    },
    {
      title: "The Way of Kings",
      author: "Brandon Sanderson",
      rating: "4.8",
      pages: "1007",
      rounded: "2.4k",
      reviewsCount: "1.1k",
      desc: "An epic fantasy masterpiece set on the storm-torn world of Roshar.",
    },
    {
      title: "A Game of Thrones",
      author: "George R.R. Martin",
      rating: "4.7",
      pages: "694",
      ratingsCount: "4.8k",
      reviewsCount: "2.3k",
      desc: "The first book in the epic fantasy series A Song of Ice and Fire.",
    },
  ],
  Romance: [
    {
      title: "Pride and Prejudice",
      author: "Jane Austen",
      rating: "4.6",
      pages: "430",
      ratingsCount: "3.2k",
      reviewsCount: "1.5k",
      desc:
        "A classic romantic novel dealing with the emotional development of Elizabeth Bennet.",
    },
    {
      title: "The Fault in Our Stars",
      author: "John Green",
      rating: "4.5",
      pages: "313",
      ratingsCount: "4.1k",
      reviewsCount: "1.9k",
      desc: "The modern love story of two teenagers dealing with cancer diagnoses.",
    },
    {
      title: "Me Before You",
      author: "Jojo Moyes",
      rating: "4.4",
      pages: "369",
      ratingsCount: "1.8k",
      reviewsCount: "750",
      desc: "A romance novel about a quirky girl taking care of a paralyzed man.",
    },
    {
      title: "Normal People",
      author: "Sally Rooney",
      rating: "4.1",
      pages: "273",
      ratingsCount: "2.2k",
      reviewsCount: "910",
      desc: "An exploration of the subtle complications of intimacy and young love.",
    },
  ],
  History: [
    {
      title: "Guns, Germs, and Steel",
      author: "Jared Diamond",
      rating: "4.5",
      pages: "425",
      ratingsCount: "1.9k",
      reviewsCount: "620",
      desc: "A book exploring the geographical factors behind global human history.",
    },
    {
      title: "The Silk Roads",
      author: "Peter Frankopan",
      rating: "4.6",
      pages: "650",
      ratingsCount: "1.1k",
      reviewsCount: "450",
      desc:
        "A major reassessment of world history, focusing on the central region of Asia.",
    },
    {
      title: "SPQR: A History of Ancient Rome",
      author: "Mary Beard",
      rating: "4.4",
      pages: "606",
      ratingsCount: "920",
      reviewsCount: "310",
      desc: "An insightful look into how a small village grew into a global empire.",
    },
    {
      title: "A People’s History",
      author: "Howard Zinn",
      rating: "4.5",
      pages: "729",
      ratingsCount: "1.5k",
      reviewsCount: "580",
      desc: "American history told from the perspective of marginalized groups.",
    },
  ],
  Biography: [
    {
      title: "Steve Jobs",
      author: "Walter Isaacson",
      rating: "4.7",
      pages: "656",
      ratingsCount: "1.8k",
      reviewsCount: "720",
      desc:
        "The exclusive biography of the creative entrepreneur who revolutionized multiple industries.",
    },
    {
      title: "Becoming",
      author: "Michelle Obama",
      rating: "4.8",
      pages: "448",
      ratingsCount: "3.5k",
      reviewsCount: "1.6k",
      desc: "An intimate, powerful, and inspiring memoir by the former First Lady.",
    },
    {
      title: "Elon Musk",
      author: "Walter Isaacson",
      rating: "4.6",
      pages: "688",
      ratingsCount: "1.2k",
      reviewsCount: "490",
      desc: "The astonishingly intimate story of the most fascinating innovator.",
    },
    {
      title: "Shoe Dog",
      author: "Phil Knight",
      rating: "4.8",
      pages: "400",
      ratingsCount: "2.7k",
      reviewsCount: "1.1k",
      desc: "A memoir by the creator of Nike, detailing the early struggle of the brand.",
    },
  ],
  "Self-Help": [
    {
      title: "Atomic Habits",
      author: "James Clear",
      rating: "4.9",
      pages: "320",
      ratingsCount: "8.5k",
      reviewsCount: "4.1k",
      desc: "An easy and proven way to build good habits and break bad ones.",
    },
    {
      title: "The Subtle Art",
      author: "Mark Manson",
      rating: "4.3",
      pages: "224",
      ratingsCount: "5.2k",
      reviewsCount: "2.1k",
      desc: "A generation-defining self-help guide to living a contented, grounded life.",
    },
    {
      title: "Deep Work",
      author: "Cal Newport",
      rating: "4.6",
      pages: "304",
      ratingsCount: "1.9k",
      reviewsCount: "740",
      desc: "Rules for focused success in a distracted world.",
    },
    {
      title: "Show Your Work!",
      author: "Austin Kleon",
      rating: "4.5",
      pages: "224",
      rounded: "1.1k",
      reviewsCount: "380",
      desc: "Ten ways to share your creativity and get discovered by others.",
    },
  ],
});
const allBooks = Object.values(booksByCategory.value).flat();

const filteredBooks = computed(() => {
  if (!searchQuery.value.trim()) return [];

  return allBooks
    .filter((book) => book.title.toLowerCase().includes(searchQuery.value.toLowerCase()))
    .slice(0, 10);
});
const toggleFavourite = (book) => {
  const index = favouriteBooks.value.findIndex((b) => b.title === book.title);

  if (index === -1) {
    favouriteBooks.value.push(book);
  } else {
    favouriteBooks.value.splice(index, 1);
  }
};

const deleteBook = (bookTitle) => {
  Object.keys(booksByCategory.value).forEach((category) => {
    booksByCategory.value[category] = booksByCategory.value[category].filter(
      (book) => book.title !== bookTitle
    );
  });
};

const addBook = () => {
  booksByCategory.value[newBook.value.category].push({
    ...newBook.value,
    rating: "5.0",
    pages: "100",
    desc: "Buku baru",
  });

  newBook.value = {
    title: "",
    author: "",
    category: "Fiction",
  };

  showAddBookModal.value = false;
};
</script>

<template>
  <div
    v-if="currentPage === 'login'"
    class="w-full min-h-screen bg-gray-100 flex items-center justify-center p-4 relative font-['Plus_Jakarta_Sans']"
  >
    <div
      class="bg-white rounded-3xl shadow-xl border border-gray-100 max-w-5xl w-full p-12 flex flex-col md:flex-row items-center justify-between min-h-[600px] relative overflow-hidden"
    >
      <div class="hidden md:block w-1/4 opacity-20">
        <div class="space-y-4">
          <div class="h-8 bg-gray-200 rounded w-3/4"></div>
          <div class="h-40 bg-gray-200 rounded"></div>
          <div class="h-24 bg-gray-200 rounded w-5/6"></div>
        </div>
      </div>

      <div class="w-full md:w-2/5 text-center z-10">
        <div
          class="flex items-center justify-center gap-2 mb-6 text-blue-600 text-2xl font-bold"
        >
          <i class="fa-solid fa-book-open-reader"></i> Library
        </div>
        <h2 class="text-2xl font-bold text-gray-800 mb-1">Akses ke Sistem</h2>
        <h2 class="text-2xl font-bold text-gray-800 mb-2">Perpustakaan</h2>
        <p class="text-sm text-gray-400 mb-8">Silakan Login</p>

        <form @submit.prevent="currentPage = 'discover'" class="text-left space-y-4">
          <div>
            <label class="text-xs font-bold text-gray-700 block mb-1.5">Email Anda</label>
            <div class="relative">
              <span class="absolute inset-y-0 left-0 flex items-center pl-4 text-gray-400"
                ><i class="fa-regular fa-envelope"></i
              ></span>
              <input
                type="email"
                placeholder="contoh: user@email.com"
                required
                class="w-full pl-11 pr-4 py-3 bg-gray-50 border border-gray-200 rounded-xl focus:bg-white focus:border-blue-500 focus:outline-none text-sm transition"
              />
            </div>
          </div>
          <div>
            <label class="text-xs font-bold text-gray-700 block mb-1.5">Kata Sandi</label>
            <div class="relative">
              <span class="absolute inset-y-0 left-0 flex items-center pl-4 text-gray-400"
                ><i class="fa-solid fa-lock"></i
              ></span>
              <input
                type="password"
                placeholder="***********"
                required
                class="w-full pl-11 pr-4 py-3 bg-gray-50 border border-gray-200 rounded-xl focus:bg-white focus:border-blue-500 focus:outline-none text-sm transition"
              />
            </div>
          </div>
          <div class="flex items-center justify-between text-xs pt-1">
            <label class="flex items-center gap-2 text-gray-500 cursor-pointer"
              ><input type="checkbox" class="rounded text-blue-600 focus:ring-blue-500" />
              Ingat Saya</label
            >
            <a href="#" class="text-blue-600 font-medium hover:underline"
              >Lupa password?</a
            >
          </div>
          <button
            type="submit"
            class="w-full bg-blue-600 hover:bg-blue-700 text-white font-bold py-3.5 rounded-xl transition shadow-lg shadow-blue-600/20 mt-4 text-sm"
          >
            LOGIN
          </button>
        </form>
        <p class="text-xs text-gray-400 mt-6">
          Belum punya akun?
          <a href="#" class="text-blue-600 font-bold hover:underline">Daftar</a>
        </p>
      </div>

      <div class="hidden md:block w-1/4 opacity-20 text-right">
        <i class="fa-solid fa-user-astronaut text-9xl text-gray-300"></i>
      </div>
    </div>
  </div>

  <div
    v-else
    class="w-full min-h-screen bg-gray-100 flex items-center justify-center p-4 font-['Plus_Jakarta_Sans'] relative"
  >
    <div
      class="bg-white rounded-3xl shadow-xl flex overflow-hidden border border-gray-100 min-h-[820px] w-full max-w-7xl relative"
    >
      <aside
        class="w-64 border-r border-gray-100 p-6 flex flex-col justify-between shrink-0 bg-white"
      >
        <div>
          <div class="flex items-center gap-3 mb-10 pl-2">
            <div class="text-blue-600 text-3xl">
              <i class="fa-solid fa-book-open-reader"></i>
            </div>
            <span class="text-2xl font-bold text-slate-800 tracking-wide">Library</span>
          </div>

          <nav class="space-y-2">
            <button
              @click="
                currentPage = 'discover';
                selectedCategory = null;
              "
              :class="
                currentPage === 'discover'
                  ? 'bg-blue-50 text-blue-600 font-semibold'
                  : 'text-gray-500 hover:bg-gray-50'
              "
              class="w-full flex items-center gap-4 px-4 py-3 rounded-xl font-medium transition text-left"
            >
              <i class="fa-solid fa-house-chimney text-lg"></i> Discover
            </button>
            <button
              @click="
                currentPage = 'category';
                selectedCategory = null;
              "
              :class="
                currentPage === 'category'
                  ? 'bg-blue-50 text-blue-600 font-semibold'
                  : 'text-gray-500 hover:bg-gray-50'
              "
              class="w-full flex items-center gap-4 px-4 py-3 rounded-xl font-medium transition text-left"
            >
              <i class="fa-solid fa-layer-group text-lg"></i> Category
            </button>
            <button
              @click="
                currentPage = 'library';
                selectedCategory = null;
              "
              :class="
                currentPage === 'library'
                  ? 'bg-blue-50 text-blue-600 font-semibold'
                  : 'text-gray-500 hover:bg-gray-50'
              "
              class="w-full flex items-center gap-4 px-4 py-3 rounded-xl font-medium transition text-left"
            >
              <i class="fa-solid fa-book text-lg"></i> My Library
            </button>
            <button
              @click="
                currentPage = 'favourite';
                selectedCategory = null;
              "
              :class="
                currentPage === 'favourite'
                  ? 'bg-blue-50 text-blue-600 font-semibold'
                  : 'text-gray-500 hover:bg-gray-50'
              "
              class="w-full flex items-center gap-4 px-4 py-3 rounded-xl font-medium transition text-left"
            >
              <i class="fa-solid fa-heart text-lg"></i> Favourite
            </button>
            <button
              @click="showAddBookModal = true"
              class="mt-6 w-full bg-blue-600 text-white py-3 rounded-xl font-semibold hover:bg-blue-700 transition"
            >
              + Tambah Buku
            </button>
          </nav>
        </div>

        <div>
          <button
            @click="showLogoutModal = true"
            class="w-full flex items-center gap-4 px-4 py-3 text-gray-500 hover:bg-red-50 hover:text-red-600 rounded-xl font-medium transition text-left"
          >
            <i class="fa-solid fa-arrow-right-from-bracket text-lg"></i> Logout
          </button>
        </div>
      </aside>

      <main class="flex-1 p-8 overflow-y-auto max-h-[820px] bg-white">
        <div class="flex justify-between items-center mb-8">
          <div class="relative">
            <i
              class="fa-solid fa-magnifying-glass absolute left-4 top-1/2 -translate-y-1/2 text-gray-400"
            ></i>

            <input
              v-model="searchQuery"
              type="text"
              placeholder="Search books..."
              class="pl-12 pr-4 py-3 border border-blue-500 rounded-2xl w-[420px] focus:outline-none"
            />
          </div>

          <div
            @click="showProfileModal = true"
            class="flex items-center gap-3 bg-gray-50 pr-4 pl-2 py-1.5 rounded-full cursor-pointer hover:bg-gray-100 transition"
          >
            <div
              class="w-8 h-8 rounded-full bg-blue-600 flex items-center justify-center text-white font-bold text-sm"
            >
              <i class="fa-regular fa-user"></i>
            </div>

            <span class="text-sm font-semibold text-gray-700">
              {{ profileName }}
            </span>

            <i class="fa-solid fa-chevron-down text-xs text-gray-400"></i>
          </div>
        </div>

        <div v-if="searchQuery" class="mb-8">
          <div
            v-if="filteredBooks.length > 0"
            class="grid grid-cols-2 md:grid-cols-4 gap-4"
          >
            <div
              v-for="book in filteredBooks"
              :key="book.title"
              @click="selectedBook = book"
              class="bg-white border border-gray-100 p-3 rounded-2xl hover:shadow-md transition cursor-pointer"
            >
              <div
                class="bg-blue-50 rounded-xl p-4 aspect-[3/4] flex items-center justify-center text-center font-bold text-xs text-blue-950 mb-3"
              >
                {{ book.title }}
              </div>

              <h3 class="font-bold text-sm text-gray-800">
                {{ book.title }}
              </h3>

              <p class="text-xs text-gray-400">
                {{ book.author }}
              </p>
            </div>
          </div>

          <div v-else class="mt-4 text-gray-400">Buku tidak ditemukan</div>
        </div>

        <div v-if="currentPage === 'discover'" class="space-y-10">
          <section>
            <div class="flex justify-between items-center mb-4">
              <h2 class="text-xl font-bold text-gray-800">Recommended</h2>
            </div>
            <div class="grid grid-cols-2 md:grid-cols-4 gap-4">
              <div
                @click="
                  selectedBook = {
                    title: 'The Psychology of Money',
                    author: 'Morgan Housel',
                    rating: '4.9',
                    pages: '250',
                    ratingsCount: '1.2k',
                    reviewsCount: '450',
                    desc:
                      'Timeless lessons on wealth, greed, and happiness doing well with money isn’t necessarily about what you know.',
                  }
                "
                :class="
                  selectedBook?.title === 'The Psychology of Money'
                    ? 'ring-2 ring-blue-500'
                    : ''
                "
                class="bg-white border border-gray-100 p-3 rounded-2xl hover:shadow-md transition cursor-pointer"
              >
                <div
                  class="bg-emerald-50 rounded-xl p-4 aspect-[3/4] flex items-center justify-center text-center font-serif text-xs font-bold text-emerald-950 mb-3"
                >
                  The Psychology of Money
                </div>
                <h3 class="font-bold text-sm text-gray-800 truncate">
                  The Psychology of...
                </h3>
                <p class="text-xs text-gray-400">Morgan Housel</p>
              </div>

              <div
                @click="
                  selectedBook = {
                    title: 'HOW INNOVATION WORKS',
                    author: 'Matt Ridley',
                    rating: '4.7',
                    pages: '300',
                    ratingsCount: '520',
                    reviewsCount: '98',
                    desc:
                      'Innovation is the main event of the modern age, the reason we experience compounding progress in our living standards.',
                  }
                "
                :class="
                  selectedBook?.title === 'HOW INNOVATION WORKS'
                    ? 'ring-2 ring-blue-500'
                    : ''
                "
                class="bg-white border border-gray-100 p-3 rounded-2xl hover:shadow-md transition cursor-pointer"
              >
                <div
                  class="bg-amber-50 rounded-xl p-4 aspect-[3/4] flex items-center justify-center text-center font-bold text-xs text-amber-900 mb-3"
                >
                  HOW INNOVATION WORKS
                </div>
                <h3 class="font-bold text-sm text-gray-800 truncate">
                  How innovation...
                </h3>
                <p class="text-xs text-gray-400">Matt Ridley</p>
              </div>

              <div
                @click="
                  selectedBook = {
                    title: 'Company of One',
                    author: 'Paul Jarvis',
                    rating: '4.8',
                    pages: '320',
                    ratingsCount: '643',
                    reviewsCount: '110',
                    desc:
                      'Company of One offers a refreshingly original business strategy that\'s focused on a commitment to being better instead of bigger.',
                  }
                "
                :class="
                  selectedBook?.title === 'Company of One' ? 'ring-2 ring-blue-500' : ''
                "
                class="bg-white border border-gray-100 p-3 rounded-2xl hover:shadow-md transition cursor-pointer"
              >
                <div
                  class="bg-gray-50 rounded-xl p-4 aspect-[3/4] flex items-center justify-center text-center font-bold text-xs text-gray-800 mb-3"
                >
                  Company of One
                </div>
                <h3 class="font-bold text-sm text-gray-800 truncate">Company of One</h3>
                <p class="text-xs text-gray-400">Paul Jarvis</p>
              </div>

              <div
                @click="
                  selectedBook = {
                    title: 'Stupore E Tremori',
                    author: 'Amélie Nothomb',
                    rating: '4.5',
                    pages: '180',
                    ratingsCount: '310',
                    reviewsCount: '65',
                    desc:
                      'A humorous yet biting semi-autobiographical novel about a Western woman navigating corporate Japan.',
                  }
                "
                :class="
                  selectedBook?.title === 'Stupore E Tremori'
                    ? 'ring-2 ring-blue-500'
                    : ''
                "
                class="bg-white border border-gray-100 p-3 rounded-2xl hover:shadow-md transition cursor-pointer"
              >
                <div
                  class="bg-rose-50 rounded-xl p-4 aspect-[3/4] flex items-center justify-center text-center font-mono text-xs text-rose-950 mb-3"
                >
                  Stupore E Tremori
                </div>
                <h3 class="font-bold text-sm text-gray-800 truncate">
                  Stupore E Tremori
                </h3>
                <p class="text-xs text-gray-400">Amélie Nothomb</p>
              </div>
            </div>
          </section>
        </div>

        <div v-if="currentPage === 'library'" class="space-y-6">
          <div
            class="w-full bg-blue-50 text-blue-700 text-center py-4 rounded-2xl font-bold text-lg"
          >
            My Library Collection
          </div>
          <div
            class="border-2 border-dashed border-gray-200 rounded-3xl p-12 text-center"
          >
            <i class="fa-solid fa-book-bookmark text-4xl text-gray-300 mb-3"></i>
            <p class="text-gray-400 text-sm">
              Belum ada buku di dalam koleksi perpustakaan kamu.
            </p>
          </div>
        </div>

        <div v-if="currentPage === 'category'" class="space-y-6">
          <div v-if="!selectedCategory" class="space-y-6">
            <div
              class="w-full bg-blue-50 text-blue-700 text-center py-4 rounded-2xl font-bold text-lg"
            >
              Browse All Categories
            </div>
            <div class="grid grid-cols-2 md:grid-cols-4 gap-6">
              <div
                @click="selectedCategory = 'Fiction'"
                class="bg-white border border-gray-100 p-6 rounded-2xl text-center cursor-pointer hover:shadow-md hover:border-blue-200 transition"
              >
                <div class="text-4xl mb-3">🧭</div>
                <h3 class="font-bold text-gray-800">Fiction</h3>
              </div>
              <div
                @click="selectedCategory = 'Non-Fiction'"
                class="bg-white border border-gray-100 p-6 rounded-2xl text-center cursor-pointer hover:shadow-md hover:border-blue-200 transition"
              >
                <div class="text-4xl mb-3">💡</div>
                <h3 class="font-bold text-gray-800">Non-Fiction</h3>
              </div>
              <div
                @click="selectedCategory = 'Science Fiction'"
                class="bg-white border border-gray-100 p-6 rounded-2xl text-center cursor-pointer hover:shadow-md hover:border-blue-200 transition"
              >
                <div class="text-4xl mb-3">🚀</div>
                <h3 class="font-bold text-gray-800">Science Fiction</h3>
              </div>
              <div
                @click="selectedCategory = 'Fantasy'"
                class="bg-white border border-gray-100 p-6 rounded-2xl text-center cursor-pointer hover:shadow-md hover:border-blue-200 transition"
              >
                <div class="text-4xl mb-3">🏰</div>
                <h3 class="font-bold text-gray-800">Fantasy</h3>
              </div>
              <div
                @click="selectedCategory = 'Romance'"
                class="bg-white border border-gray-100 p-6 rounded-2xl text-center cursor-pointer hover:shadow-md hover:border-blue-200 transition"
              >
                <div class="text-4xl mb-3">💖</div>
                <h3 class="font-bold text-gray-800">Romance</h3>
              </div>
              <div
                @click="selectedCategory = 'History'"
                class="bg-white border border-gray-100 p-6 rounded-2xl text-center cursor-pointer hover:shadow-md hover:border-blue-200 transition"
              >
                <div class="text-4xl mb-3">🏛️</div>
                <h3 class="font-bold text-gray-800">History</h3>
              </div>
              <div
                @click="selectedCategory = 'Biography'"
                class="bg-white border border-gray-100 p-6 rounded-2xl text-center cursor-pointer hover:shadow-md hover:border-blue-200 transition"
              >
                <div class="text-4xl mb-3">✒️</div>
                <h3 class="font-bold text-gray-800">Biography</h3>
              </div>
              <div
                @click="selectedCategory = 'Self-Help'"
                class="bg-white border border-gray-100 p-6 rounded-2xl text-center cursor-pointer hover:shadow-md hover:border-blue-200 transition"
              >
                <div class="text-4xl mb-3">🌳</div>
                <h3 class="font-bold text-gray-800">Self-Help</h3>
              </div>
            </div>
          </div>

          <div v-else class="space-y-6">
            <div class="flex items-center justify-between">
              <div class="flex items-center gap-2">
                <button
                  @click="selectedCategory = null"
                  class="text-blue-600 hover:text-blue-800 font-medium text-sm flex items-center gap-1 bg-blue-50 px-3 py-1.5 rounded-xl transition"
                >
                  <i class="fa-solid fa-arrow-left"></i> Kembali ke Kategori
                </button>
              </div>
              <h2 class="text-xl font-bold text-gray-800">
                Kategori: <span class="text-blue-600">{{ selectedCategory }}</span>
              </h2>
            </div>

            <div class="grid grid-cols-2 md:grid-cols-4 gap-4">
              <div
                v-for="book in booksByCategory[selectedCategory]"
                :key="book.title"
                @click="selectedBook = book"
                :class="selectedBook?.title === book.title ? 'ring-2 ring-blue-500' : ''"
                class="bg-white border border-gray-100 p-3 rounded-2xl hover:shadow-md transition cursor-pointer"
              >
                <div
                  class="bg-blue-50/70 rounded-xl p-4 aspect-[3/4] flex items-center justify-center text-center font-bold text-xs text-blue-950 mb-3 shadow-inner uppercase line-clamp-3"
                >
                  {{ book.title }}
                </div>
                <h3 class="font-bold text-sm text-gray-800 truncate">{{ book.title }}</h3>
                <p class="text-xs text-gray-400 truncate">{{ book.author }}</p>
              </div>
            </div>

            <div
              v-if="
                !booksByCategory[selectedCategory] ||
                booksByCategory[selectedCategory].length === 0
              "
              class="text-center py-10 text-gray-400 text-sm"
            >
              Belum ada koleksi buku di kategori ini.
            </div>
          </div>
        </div>

        <div v-if="currentPage === 'favourite'" class="space-y-6">
          <h2 class="text-xl font-bold text-gray-800">My Favourite Collection</h2>
          <div class="grid grid-cols-2 md:grid-cols-4 gap-4">
            <div class="bg-white border border-gray-100 p-3 rounded-2xl text-center">
              <div
                class="bg-slate-900 text-amber-400 aspect-[3/4] rounded-xl flex items-center justify-center font-serif font-black text-center p-4 mb-2"
              >
                PROJECT HAIL MARY
              </div>
              <h4 class="text-xs font-bold text-gray-800">Project Hail Mary</h4>
              <p class="text-[10px] text-gray-400">Andy Weir</p>
            </div>
            <div class="bg-white border border-gray-100 p-3 rounded-2xl text-center">
              <div
                class="bg-orange-200 text-orange-900 aspect-[3/4] rounded-xl flex items-center justify-center font-bold text-center p-4 mb-2"
              >
                WHERE THE CRAWDADS SING
              </div>
              <h4 class="text-xs font-bold text-gray-800">Crawdads Sing</h4>
              <p class="text-[10px] text-gray-400">Delia Owens</p>
            </div>
            <div class="bg-white border border-gray-100 p-3 rounded-2xl text-center">
              <div
                class="bg-yellow-50 text-yellow-900 aspect-[3/4] rounded-xl flex items-center justify-center font-bold text-center p-4 mb-2"
              >
                Sapiens
              </div>
              <h4 class="text-xs font-bold text-gray-800">Sapiens</h4>
              <p class="text-[10px] text-gray-400">Yuval Noah</p>
            </div>
            <div class="bg-white border border-gray-100 p-3 rounded-2xl text-center">
              <div
                class="bg-blue-900 text-white aspect-[3/4] rounded-xl flex items-center justify-center font-bold text-center p-4 mb-2"
              >
                THINKING, FAST AND SLOW
              </div>
              <h4 class="text-xs font-bold text-gray-800">Thinking, Fast/Slow</h4>
              <p class="text-[10px] text-gray-400">Daniel Kahneman</p>
            </div>
          </div>
        </div>
      </main>

      <aside
        v-if="selectedBook"
        class="w-80 bg-slate-950 text-white p-6 flex flex-col justify-between shrink-0 transition-all"
      >
        <div>
          <div class="flex items-center justify-between mb-6">
            <span class="text-xs text-gray-400 font-medium block"
              >Selected Book Detail</span
            >
            <button
              @click="selectedBook = null"
              class="text-xs text-gray-400 hover:text-white flex items-center gap-1 transition"
            >
              Tutup <i class="fa-solid fa-xmark"></i>
            </button>
          </div>

          <div
            class="bg-white text-slate-900 rounded-2xl p-6 aspect-[3/4] flex flex-col justify-between mb-6 shadow-2xl max-w-[180px] mx-auto"
          >
            <div class="border-b border-gray-100 pb-2 text-center">
              <h1 class="text-lg font-serif font-bold leading-tight line-clamp-3">
                {{ selectedBook.title }}
              </h1>
            </div>
            <div
              class="text-center text-[10px] uppercase text-gray-400 font-bold truncate"
            >
              {{ selectedBook.author }}
            </div>
          </div>

          <div class="text-center mb-6">
            <h3 class="text-base font-bold line-clamp-2">{{ selectedBook.title }}</h3>
            <p class="text-xs text-gray-400 mt-0.5">{{ selectedBook.author }}</p>
            <div
              class="flex items-center justify-center gap-1 mt-2 text-amber-400 text-xs"
            >
              <i class="fa-solid fa-star"></i><i class="fa-solid fa-star"></i
              ><i class="fa-solid fa-star"></i><i class="fa-solid fa-star"></i
              ><i class="fa-solid fa-star"></i>
              <span class="text-white ml-1 font-bold">{{
                selectedBook.rating || "4.5"
              }}</span>
            </div>
          </div>

          <div
            class="grid grid-cols-3 gap-1 text-center bg-slate-900 p-2 rounded-xl text-xs border border-slate-800 mb-6"
          >
            <div>
              <div class="font-bold">{{ selectedBook.pages || "-" }}</div>
              <div class="text-[9px] text-gray-400">Pages</div>
            </div>
            <div class="border-x border-slate-800">
              <div class="font-bold">{{ selectedBook.ratingsCount || "-" }}</div>
              <div class="text-[9px] text-gray-400">Ratings</div>
            </div>
            <div>
              <div class="font-bold">{{ selectedBook.reviewsCount || "-" }}</div>
              <div class="text-[9px] text-gray-400">Reviews</div>
            </div>
          </div>

          <p class="text-xs text-gray-400 leading-relaxed line-clamp-4">
            {{ selectedBook.desc }}
          </p>
        </div>

        <button
          class="w-full bg-blue-600 hover:bg-blue-700 py-3 rounded-xl font-bold text-xs flex items-center justify-center gap-2 transition shadow-lg mt-4"
        >
          Read Now <i class="fa-solid fa-book-open"></i>
        </button>
      </aside>

      <div
        v-if="showProfileModal"
        class="absolute inset-0 bg-black/60 backdrop-blur-sm flex items-center justify-center z-50 p-4"
      >
        <div
          class="bg-white rounded-3xl p-6 max-w-sm w-full shadow-2xl relative text-slate-800"
        >
          <h3 class="text-gray-400 text-xs font-bold tracking-wider mb-4">
            Profil Anggota
          </h3>
          <div class="flex flex-col items-center text-center mb-6">
            <div
              class="w-20 h-20 rounded-full bg-gray-100 text-blue-600 text-4xl flex items-center justify-center mb-3 shadow-inner"
            >
              <i class="fa-regular fa-user"></i>
            </div>
            <h2 class="text-xl font-bold text-slate-800">{{ profileName }}</h2>
            <p class="text-xs text-blue-600 font-medium">
              {{ profileEmail }}
            </p>
          </div>
          <div class="space-y-4 mb-6">
            <div>
              <label class="text-xs font-bold text-gray-500 block mb-1">
                Nama Lengkap
              </label>
              <input
                type="text"
                v-model="profileName"
                class="w-full px-4 py-2.5 bg-gray-50 border border-gray-200 rounded-xl text-sm focus:bg-white focus:border-blue-500 focus:outline-none font-medium transition"
              />
            </div>

            <div>
              <label class="text-xs font-bold text-gray-500 block mb-1"> Email </label>
              <input
                type="email"
                v-model="profileEmail"
                class="w-full px-4 py-2.5 bg-gray-50 border border-gray-200 rounded-xl text-sm focus:bg-white focus:border-blue-500 focus:outline-none font-medium transition"
              />
            </div>

            <div>
              <label class="text-xs font-bold text-gray-500 block mb-1">
                Biodata Singkat
              </label>
              <textarea
                v-model="profileBio"
                class="w-full px-4 py-2.5 bg-gray-50 border border-gray-200 rounded-xl text-sm focus:bg-white focus:border-blue-500 focus:outline-none h-24 resize-none font-medium leading-relaxed transition"
              ></textarea>
            </div>
          </div>

          <div class="flex gap-2">
            <button
              @click="showProfileModal = false"
              class="w-full bg-blue-600 hover:bg-blue-700 text-white font-bold py-3 rounded-xl text-sm transition"
            >
              Simpan & Tutup
            </button>
          </div>
        </div>
      </div>

      <div
        v-if="showLogoutModal"
        class="absolute inset-0 bg-black/60 backdrop-blur-sm flex items-center justify-center z-50 p-4"
      >
        <div
          class="bg-white rounded-3xl p-6 max-xs w-full shadow-2xl text-center text-slate-800"
        >
          <div
            class="w-12 h-12 bg-amber-50 text-amber-500 rounded-full flex items-center justify-center text-xl mx-auto mb-4"
          >
            <i class="fa-solid fa-triangle-exclamation"></i>
          </div>
          <h3 class="text-lg font-bold mb-1">Ingin Logout?</h3>
          <p class="text-xs text-gray-400 leading-relaxed mb-6">
            Sesi Anda akan berakhir dan Anda harus login kembali.
          </p>
          <div class="flex gap-3">
            <button
              @click="showLogoutModal = false"
              class="flex-1 bg-gray-100 hover:bg-gray-200 text-gray-600 font-bold py-2.5 rounded-xl text-xs transition"
            >
              BATAL
            </button>
            <button
              @click="
                () => {
                  showLogoutModal = false;
                  currentPage = 'login';
                }
              "
              class="flex-1 bg-blue-600 hover:bg-blue-700 text-white font-bold py-2.5 rounded-xl text-xs transition flex items-center justify-center gap-1"
            >
              LOGOUT <i class="fa-solid fa-arrow-right-from-bracket text-[10px]"></i>
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
