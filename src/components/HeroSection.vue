<template>
  <div class="relative max-w-7xl mx-auto px-6 py-24">
    <div class="flex flex-col lg:flex-row items-center">
      <!-- Left Side -->
      <div class="w-full lg:w-1/2 mb-12 lg:mb-0">
        <h2 class="text-5xl lg:text-6xl font-bold leading-tight mb-6">
          Crea tours
          <span
            class="bg-gradient-to-r from-purple-400 to-pink-600 text-transparent bg-clip-text"
            >interactivos</span
          >
          para tus app web en vue
        </h2>
        <p class="text-gray-300 text-xl mb-8">
          TuturVue: Un componente reutilizable para crear tours de usuario en
          Vue 3.
        </p>
        <div
          class="flex flex-col sm:flex-row items-center space-y-4 sm:space-y-0 sm:space-x-4"
        >
          <a
            id="btn-how-to-use"
            href="#como-usar"
            class="bg-gradient-to-r from-purple-500 to-pink-600 hover:from-purple-600 hover:to-pink-700 px-8 py-3 rounded-full font-medium flex items-center justify-center w-full sm:w-auto transition-all duration-200 transform hover:scale-105"
          >
            Cómo Usar
            <ArrowRightIcon class="h-5 w-5 ml-2" />
          </a>
          <a
            href="#ejemplos"
            class="bg-gray-800 hover:bg-gray-700 px-8 py-3 rounded-full font-medium flex items-center justify-center w-full sm:w-auto border border-gray-700 hover:border-gray-600 transition-all duration-200"
          >
            Ver Ejemplos
          </a>
        </div>
      </div>

      <!-- Right Side -->
      <div class="w-full lg:w-1/2 lg:pl-12">
        <!-- Demo Card -->
        <div
          class="bg-gray-800/50 backdrop-blur-sm rounded-2xl p-8 shadow-2xl transform hover:scale-105 transition-all duration-300"
        >
          <div class="flex items-center justify-between mb-6">
            <div class="flex items-center space-x-4">
              <div
                class="w-12 h-12 bg-gradient-to-br from-purple-500 to-pink-600 rounded-full flex items-center justify-center"
              >
                <MapIcon class="h-6 w-6 text-white" />
              </div>
              <div>
                <h3 class="font-semibold text-lg">Tour de Bienvenida</h3>
                <p class="text-gray-400 text-sm">TuturVue Demo</p>
              </div>
            </div>
            <button
              class="bg-purple-600 hover:bg-purple-700 px-4 py-2 rounded-full text-sm font-medium transition-colors duration-200"
            >
              Iniciar Tour
            </button>
          </div>
          <p class="text-gray-300 text-sm mb-6">
            Guía a tus usuarios a través de tu aplicación con elegantes tours
            interactivos.
          </p>
          <div class="flex items-center space-x-4 text-sm text-gray-400">
            <span class="flex items-center">
              <ClockIcon class="h-4 w-4 mr-1" />
              3 Pasos
            </span>
            <span class="flex items-center">
              <TimerIcon class="h-4 w-4 mr-1" />
              2 min de duración
            </span>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ArrowRightIcon, MapIcon, ClockIcon, TimerIcon } from "lucide-vue-next";
</script>
