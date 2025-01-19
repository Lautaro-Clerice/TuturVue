<template>
  <div id="caracteristicas" class="max-w-7xl mx-auto px-6 py-24">
    <h2 class="text-4xl font-bold mb-12 text-center">
      Características Principales
    </h2>
    <div
      id="feature-section"
      class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-8"
    >
      <div
        v-for="feature in features"
        :key="feature.title"
        class="bg-gray-800/50 backdrop-blur-sm rounded-2xl p-6 shadow-xl transform hover:scale-105 transition-all duration-300"
      >
        <div class="flex items-center space-x-3 mb-4">
          <div
            class="w-10 h-10 bg-gradient-to-br from-purple-500 to-pink-600 rounded-full flex items-center justify-center"
          >
            <component :is="feature.icon" class="h-5 w-5 text-white" />
          </div>
          <h3 class="font-semibold text-lg">{{ feature.title }}</h3>
        </div>
        <p class="text-gray-300 text-sm">
          {{ feature.description }}
        </p>
      </div>
    </div>
  </div>
</template>

<script setup>
import { MapPinIcon, ZapIcon, PaletteIcon, LayoutIcon } from "lucide-vue-next";

const features = [
  {
    title: "Intuitivo",
    description:
      "Crea tours de usuario fácilmente con una configuración simple.",
    icon: MapPinIcon,
  },
  {
    title: "Rápido",
    description: "Optimizado para Vue 3, con excelente rendimiento.",
    icon: ZapIcon,
  },
  {
    title: "Personalizable",
    description: "Adapta el diseño a tu marca con opciones de personalización.",
    icon: PaletteIcon,
  },
  {
    title: "Responsivo",
    description:
      "Funciona perfectamente en dispositivos móviles y de escritorio.",
    icon: LayoutIcon,
  },
];
</script>
