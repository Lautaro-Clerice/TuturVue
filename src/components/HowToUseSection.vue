<template>
  <div id="como-usar" class="max-w-7xl mx-auto px-6 py-24">
    <h2 class="text-4xl font-bold mb-12 text-center">Cómo Usar TuturVue</h2>
    <div
      class="bg-gray-800/50 backdrop-blur-sm rounded-2xl p-8 shadow-2xl"
      id="documentation"
    >
      <div class="space-y-8">
        <div>
          <h3 class="text-2xl font-semibold mb-4">1. Instala el componente</h3>
          <p class="text-gray-300 mb-4">
            Agrega el archivo
            <code class="bg-gray-700 px-2 py-1 rounded">TuturVue.vue</code> en
            tu proyecto.
          </p>
          <p class="text-gray-300">
            Luego, importa el componente en el archivo donde desees usarlo:
          </p>
          <pre class="bg-gray-900 p-4 rounded-lg overflow-x-auto">
<code class="language-javascript">
import TuturVue from './components/TuturVue.vue';
</code>
          </pre>
        </div>
        <div>
          <h3 class="text-2xl font-semibold mb-4">
            2. Configura los pasos del tour
          </h3>
          <p class="text-gray-300 mb-4">
            Define un arreglo llamado <code>steps</code> en el que describas los
            pasos del tour. Cada paso puede incluir las siguientes propiedades:
          </p>
          <ul class="list-disc list-inside text-gray-300 mb-4">
            <li>
              <code>id</code>: El id del elemento que se destacará en ese paso.
            </li>
            <li>
              <code>title</code>: Un título que se mostrará para el paso. Puede
              contener HTML (por ejemplo, un ícono o imagen).
            </li>
            <li><code>content</code>: La descripción o mensaje del paso.</li>
            <li>
              <code>attachTo</code>: Configura a qué elemento se debe adjuntar
              el paso (por ejemplo, el selector del elemento y la posición).
              <ul class="list-disc list-inside ml-6">
                <li>
                  <code>element</code>: Selector del elemento que se debe
                  resaltar.
                </li>
                <li>
                  <code>on</code>: La posición del tooltip en relación con el
                  elemento (<code>"top"</code>, <code>"bottom"</code>,
                  <code>"left"</code>, <code>"right"</code>).
                </li>
              </ul>
            </li>
            <li>
              <code>position</code>: La posición del contenido del paso en
              relación con el elemento destacado (top, bottom, left, right).
            </li>
            <li>
              <code>media</code>: (Opcional) Incluye imágenes o videos.
              Estructura:
              <ul class="list-disc list-inside ml-6">
                <li>
                  <code>type</code>: Tipo de medio (<code>"image"</code> o
                  <code>"video"</code>).
                </li>
                <li><code>src</code>: URL de la imagen o video.</li>
                <li><code>alt</code>: Texto alternativo.</li>
                <li>
                  <code>controls</code>: (boolean) Muestra los controles del
                  video.
                </li>
              </ul>
            </li>
            <li>
              <code>beforeShowPromise</code>: (Opcional) Una función que se
              ejecuta antes de mostrar el paso, por ejemplo, para desplazar el
              elemento a la vista.
            </li>
            <li>
              <code>onNext</code>: (Opcional) Una función que se ejecuta al
              avanzar al siguiente paso.
            </li>
            <li>
              <code>onBack</code>: (Opcional) Una función que se ejecuta al
              retroceder al paso anterior.
            </li>
            <li>
              <code>onFinish</code>: (Opcional) Una función que se ejecuta
              cuando se completa el tour.
            </li>
          </ul>
          <p class="text-gray-300 mb-4">Ejemplo básico de configuración:</p>
          <pre class="bg-gray-900 p-4 rounded-lg overflow-x-auto">
<code class="language-javascript">
const steps = [
  {
    id: "step1",
    title: "Bienvenido < img src='${gitIcon}' alt='icon' />",
    content: "Este es el primer paso. Aquí puedes explicar esta sección.",
    attachTo: {
      element: "#step1", // Selector del elemento
      on: "bottom", // Tooltip en la parte inferior
    },
    position: "bottom",
    beforeShowPromise: () => scrollToElement("#step1"),
  },
  {
    id: "step2",
    title: "Explora",
    content: "Este es el segundo paso. Proporciona información adicional aquí.",
    attachTo: {
      element: "#step2",
      on: "top", // Tooltip en la parte superior
    },
    position: "top",
    onNext: () => console.log("Avanzando al siguiente paso."),
    onBack: () => console.log("Regresando al paso anterior."),
  },
];
</code>
          </pre>
        </div>
        <div>
          <h3 class="text-2xl font-semibold mb-4">
            3. Usa el componente en tu template
          </h3>
          <p class="text-gray-300 mb-4">
            Utiliza el componente <code>TuturVue</code> en tu template, pasando
            las siguientes props:
          </p>
          <ul class="list-disc list-inside text-gray-300 mb-4">
            <li><code>:steps</code>: El arreglo con los pasos del tour.</li>
            <li>
              <code>:isVisible</code>: Controla si el tour está activo o no
              (<code>boolean</code>).
            </li>
            <li>
              <code>@end</code>: Escucha el evento que se dispara cuando el tour
              finaliza.
            </li>
            <li>
              <code>@step-change</code>: Escucha el evento que se dispara cuando
              cambia el paso.
            </li>
          </ul>
          <pre class="bg-gray-900 p-4 rounded-lg overflow-x-auto">
<code class="language-vue">
< template>
  < div>
    < TuturVue :steps="steps" :isVisible="showTour" @end="handleTourEnd" @step-change="handleStepChange" />
  < /div>
< /template>
</code>
          </pre>
        </div>
        <div>
          <h3 class="text-2xl font-semibold mb-4">
            4. Controla la visibilidad del tour
          </h3>
          <p class="text-gray-300 mb-4">
            Usa una variable reactiva, como <code>showTour</code>, para activar
            o detener el tour. Puedes iniciarlo con un botón o cualquier evento.
          </p>
          <pre class="bg-gray-900 p-4 rounded-lg overflow-x-auto">
<code class="language-javascript">
import { ref } from 'vue';

const showTour = ref(true);

const handleTourEnd = () => {
  console.log("El tour ha finalizado");
  showTour.value = false; // Desactiva el tour
};

const handleStepChange = (currentStep) => {
  console.log("Paso actual:", currentStep);
};
</code>
          </pre>
        </div>
        <div>
          <h3 class="text-2xl font-semibold mb-4">
            5. Personaliza más el tour
          </h3>
          <p class="text-gray-300 mb-4">
            Puedes incluir elementos avanzados como videos, imágenes o efectos
            personalizados. Ejemplo con un video:
          </p>
          <pre class="bg-gray-900 p-4 rounded-lg overflow-x-auto">
<code class="language-javascript">
const steps = [
  {
    id: "step3",
    title: "Con un video",
    content: "Este paso incluye un video de ejemplo.",
    media: {
      type: "video",
      src: "https://example.com/video.mp4",
      alt: "Descripción del video",
      controls: true,
    },
  },
];
</code>
          </pre>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
// Esta página solo sirve para explicar cómo usar el componente TuturVue.
</script>
