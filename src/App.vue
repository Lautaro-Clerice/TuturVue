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
      <HeroSection />
      <FeaturesSection />
      <HowToUseSection />
      <ExamplesSection />
    </div>
  </div>
</template>

<script setup>
import TheNavigation from "./components/TheNavigation.vue";
import HeroSection from "./components/HeroSection.vue";
import FeaturesSection from "./components/FeaturesSection.vue";
import HowToUseSection from "./components/HowToUseSection.vue";
import ExamplesSection from "./components/ExamplesSection.vue";
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

/* Ensure smooth scrolling */
html {
  scroll-behavior: smooth;
}

/* Code highlighting */
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
