<template>
  <nav
    class="border-b border-gray-800 px-4 lg:px-6 py-4 backdrop-blur-md bg-gray-900/70 sticky top-0 z-50"
  >
    <div class="max-w-7xl mx-auto flex items-center justify-between">
      <div class="flex items-center space-x-4">
        <h1
          class="text-2xl font-bold bg-gradient-to-r from-purple-400 to-pink-600 text-transparent bg-clip-text"
        >
          TuturVue
        </h1>
        <span
          class="text-sm bg-purple-800/50 px-2 py-1 rounded-full hidden sm:inline-block"
          >v1.0.0</span
        >
      </div>
      <div class="hidden md:flex items-center space-x-6">
        <a
          v-for="item in navItems"
          :key="item.href"
          :href="item.href"
          class="text-gray-300 hover:text-purple-400 transition-colors duration-200"
        >
          {{ item.text }}
        </a>

        <a
          href="https://github.com/Lautaro-Clerice/TuturVue"
          class="flex items-center space-x-1 bg-gray-800/50 rounded-full px-4 py-2 hover:bg-gray-700/50 transition-colors duration-200"
        >
          <GithubIcon class="h-5 w-5" />
        </a>
      </div>
      <button
        @click="toggleMobileMenu"
        class="md:hidden text-gray-300 hover:text-purple-400 transition-colors duration-200"
      >
        <MenuIcon v-if="!mobileMenuOpen" class="h-6 w-6" />
        <XIcon v-else class="h-6 w-6" />
      </button>
    </div>
    <!-- Menú móvil -->
    <div
      v-if="mobileMenuOpen"
      class="md:hidden mt-4 space-y-2 animate-fade-in-down"
    >
      <a
        v-for="item in navItems"
        :key="item.href"
        :href="item.href"
        class="block py-2 px-4 text-gray-300 hover:bg-gray-800/50 rounded-lg transition-colors duration-200"
      >
        {{ item.text }}
      </a>

      <a
        href="https://github.com/Lautaro-Clerice/TuturVue"
        class="flex items-center space-x-1 bg-gray-800/50 rounded-full px-4 py-2 mt-4 hover:bg-gray-700/50 transition-colors duration-200"
      >
        <GithubIcon class="h-5 w-5" />
      </a>
    </div>
  </nav>
</template>

<script setup>
import { ref } from "vue";
import { SearchIcon, GithubIcon, MenuIcon, XIcon } from "lucide-vue-next";

const mobileMenuOpen = ref(false);

const toggleMobileMenu = () => {
  mobileMenuOpen.value = !mobileMenuOpen.value;
};

const navItems = [
  { text: "Características", href: "#caracteristicas" },
  { text: "Cómo Usar", href: "#como-usar" },
  { text: "Ejemplos", href: "#ejemplos" },
];
</script>

<style scoped>
.animate-fade-in-down {
  animation: fadeInDown 0.3s ease-out;
}

@keyframes fadeInDown {
  from {
    opacity: 0;
    transform: translateY(-10px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
</style>
