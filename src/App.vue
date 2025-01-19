<template>
  <div class="min-h-screen bg-gray-900 text-white relative overflow-hidden">
    <!-- Gradient Mesh Background -->
    <div class="fixed inset-0 overflow-hidden pointer-events-none">
      <div
        class="absolute inset-0 bg-gradient-to-br from-purple-900/50 via-gray-900 to-gray-900"
      >
        <div
          class="absolute inset-0 bg-[radial-gradient(ellipse_at_top,_var(--tw-gradient-stops))] from-purple-800/20 via-gray-900 to-transparent"
        ></div>
      </div>
    </div>

    <!-- Content Wrapper -->
    <div class="relative z-10">
      <TheNavigation />
      <HeroSection @startTour="startTour" />
      <FeaturesSection />
      <HowToUseSection />
      <ExamplesSection />
    </div>
    <TuturVue :steps="tourSteps" :isVisible="showTour" />
  </div>
</template>

<script setup>
import TheNavigation from "./components/TheNavigation.vue";
import HeroSection from "./components/HeroSection.vue";
import FeaturesSection from "./components/FeaturesSection.vue";
import HowToUseSection from "./components/HowToUseSection.vue";
import ExamplesSection from "./components/ExamplesSection.vue";
import TuturVue from "./components/TuturVue.vue";
import { ref } from "vue";
import tuturVue from "./assets/tuturVue.png";
const showTour = ref(false);
const startTour = () => {
  showTour.value = true;
};

const tourSteps = [
  {
    id: "btn-how-to-use",
    title: `
      Como usar el componente TuturVue
    `,
    content: "Al hacer click sobre el podrás visualizar la documentación",
    media: {
      type: "image",
      src: tuturVue,
      alt: "Logo TuturVue",
    },
    attachTo: {
      element: "#btn-how-to-use",
      on: "bottom",
    },

    beforeShowPromise: () => scrollToElement("#btn-how-to-use"),
    position: "right",
  },
  {
    id: "feature-section",
    title: `
      En esta sección podés ver lo mejor de este componente
    `,
    content: "Enterate de todo lo que contiene TuturVue",
    attachTo: {
      element: "#feature-section",
    },

    beforeShowPromise: () => scrollToElement("#feature-section"),
    position: "bottom",
  },

  {
    id: "documentation",
    title: `
      Esta es la sección de documentación
    `,
    content:
      "Acá podes ver todas las props aceptadas y formas de uso del componente",
    attachTo: {
      element: "#documentation",
      on: "bottom",
    },

    beforeShowPromise: () => scrollToElement("#documentation"),
    position: "right",
  },
  {
    id: "examples-section",
    title: `
      Sección de ejemplos
    `,
    content: "Utilizá como recurso estos ejemplos para crear tus propios tours",
    attachTo: {
      element: "#examples-section",
    },

    beforeShowPromise: () => scrollToElement("#examples-section"),
    position: "bottom",
    onFinish: () => {
      showTour.value = false;
    },
  },
];
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap");

body {
  font-family: "Inter", sans-serif;
}

/* Custom scrollbar for modern browsers */
::-webkit-scrollbar {
  width: 8px;
  height: 8px;
}

::-webkit-scrollbar-track {
  background: #1a1a1a;
}

::-webkit-scrollbar-thumb {
  background: #4a4a4a;
  border-radius: 4px;
}

::-webkit-scrollbar-thumb:hover {
  background: #555;
}

html {
  scroll-behavior: smooth;
}

pre {
  background-color: #1e1e1e;
  border-radius: 0.5rem;
  padding: 1rem;
}

code {
  font-family: "Fira Code", monospace;
  color: #d4d4d4;
}

.language-vue .token.tag,
.language-javascript .token.keyword {
  color: #569cd6;
}

.language-vue .token.attr-name,
.language-javascript .token.string {
  color: #9cdcfe;
}

.language-vue .token.attr-value,
.language-javascript .token.number {
  color: #ce9178;
}

.language-vue .token.punctuation,
.language-javascript .token.punctuation {
  color: #d4d4d4;
}

.language-javascript .token.operator {
  color: #d4d4d4;
}

.language-javascript .token.comment {
  color: #6a9955;
}
</style>
