<template>
  <div id="ejemplos" class="max-w-7xl mx-auto px-6 py-24">
    <h2 class="text-4xl font-bold mb-12 text-center">Ejemplos de Uso</h2>
    <div class="grid grid-cols-1 md:grid-cols-2 gap-8">
      <div
        v-for="example in examples"
        :key="example.title"
        class="bg-gray-800/50 backdrop-blur-sm rounded-2xl p-8 shadow-2xl"
      >
        <h3 class="text-2xl font-semibold mb-4">{{ example.title }}</h3>
        <pre class="bg-gray-900 p-4 rounded-lg overflow-x-auto">
<code class="language-javascript">{{ example.code }}</code>
        </pre>
      </div>
    </div>
  </div>
</template>

<script setup>
const examples = [
  // Ejemplo 1: Agregar a Favoritos
  {
    title: "Tour: Agregar a Favoritos",
    code: `const favoritesTour = [
  {
    id: "add-favorites",
    title: \`
      <img src="\${gitIcon}" alt="favorites" />
      Aprende a guardar en Favoritos
    \`,
    content: "Haz clic en el ícono de estrella para agregar este artículo a tu lista de favoritos.",
    attachTo: { element: "#add-favorites", on: "bottom" },
    media: {
      type: "image",
      src: "https://via.placeholder.com/300",
      alt: "Vista previa de la funcionalidad",
    },
    beforeShowPromise: () => scrollToElement("#add-favorites"),
    position: "right",
  },
  {
    id: "view-favorites",
    title: "Accede a tus Favoritos",
    content: "Haz clic en la sección de Favoritos en el menú superior para ver lo que guardaste.",
    attachTo: { element: "#view-favorites", on: "top" },
    position: "top",
  },
];`,
  },

  // Ejemplo 2: Tutorial de Registro
  {
    title: "Tour: Tutorial de Registro",
    code: `const registrationTour = [
  {
    id: "fill-details",
    title: "Completa tu Información",
    content: "Llena los campos obligatorios como nombre, correo y contraseña para continuar.",
    attachTo: { element: "#registration-form", on: "bottom" },
    position: "bottom",
  },
  {
    id: "submit-registration",
    title: "Envía tu Registro",
    content: "Haz clic en el botón 'Registrarse' para completar tu proceso de registro.",
    attachTo: { element: "#submit-registration", on: "right" },
    position: "right",
  },
  {
    id: "confirm-email",
    title: "Confirma tu Correo",
    content: "Revisa tu correo electrónico y haz clic en el enlace de confirmación para activar tu cuenta.",
    media: {
      type: "video",
      src: "https://res.cloudinary.com/dizqvnfsj/video/upload/v1731098410/ey8zoebrwfxhc2nfhxzt.mp4",
      alt: "Vista de la bandeja de entrada",
      controls: true,
    },
    attachTo: { element: "#email-confirmation", on: "bottom" },
    position: "left",
  },
];`,
  },

  // Ejemplo 3: Tutorial de Configuración de Cuenta
  {
    title: "Tour: Configuración de Cuenta",
    code: `const accountSettingsTour = [
  {
    id: "update-profile",
    title: "Actualiza tu Perfil",
    content: "Cambia tu foto de perfil, tu nombre o tus preferencias desde esta sección.",
    attachTo: { element: "#profile-section", on: "top" },
    position: "top",
  },
  {
    id: "change-password",
    title: "Cambia tu Contraseña",
    content: "Por seguridad, puedes actualizar tu contraseña periódicamente desde aquí.",
    attachTo: { element: "#password-settings", on: "right" },
    media: {
      type: "image",
      src: "https://via.placeholder.com/500",
      alt: "Pantalla de cambio de contraseña",
    },
    position: "right",
  },
  {
    id: "enable-2fa",
    title: "Habilita 2FA",
    content: "Activa la autenticación de dos factores para añadir una capa extra de seguridad a tu cuenta.",
    attachTo: { element: "#two-factor-auth", on: "bottom" },
    beforeShowPromise: () => scrollToElement("#two-factor-auth"),
    position: "bottom",
  },
];`,
  },

  // Ejemplo 4: Descubriendo Funcionalidades Avanzadas
  {
    title: "Tour: Funcionalidades Avanzadas",
    code: `const advancedFeaturesTour = [
  {
    id: "analytics-dashboard",
    title: "Análisis Avanzados",
    content: "Explora gráficos interactivos y estadísticas detalladas de tus datos.",
    attachTo: { element: "#analytics-dashboard", on: "bottom" },
    media: {
      type: "video",
      src: "https://res.cloudinary.com/dizqvnfsj/video/upload/v1731098410/ey8zoebrwfxhc2nfhxzt.mp4",
      alt: "Demostración de análisis",
      controls: true,
    },
    position: "bottom",
  },
  {
    id: "custom-reports",
    title: "Reportes Personalizados",
    content: "Crea y descarga reportes personalizados según tus necesidades.",
    attachTo: { element: "#custom-reports", on: "top" },
    position: "top",
  },
];`,
  },
];
</script>
