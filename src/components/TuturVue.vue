<template>
  <Transition name="fade">
    <div v-if="isVisible" class="tour-overlay">
      <div
        class="tour-overlay-mask"
        :style="maskStyle"
        @click="handleOverlayClick"
      ></div>

      <TransitionGroup name="step" tag="div">
        <div
          v-for="(step, index) in steps"
          :key="index"
          v-show="currentStep === index && !isStepHidden"
          class="tour-step"
          :class="{
            'tour-step-mobile': isMobile,
            'tour-step-small-height': isSmallHeight,
          }"
          :style="getStepStyle(step)"
          @click.stop
        >
          <div class="tour-step-content">
            <h3 v-html="step.title" class="tour-step-title"></h3>

            <div v-if="step.media" class="tour-media">
              <img
                v-if="step.media.type === 'image'"
                :src="step.media.src"
                :alt="step.media.alt || ''"
                class="tour-image"
              />
              <video
                v-else-if="step.media.type === 'video'"
                :src="step.media.src"
                autoplay
                :controls="step.media.controls !== false"
                loop
                muted
                class="tour-video"
              ></video>
            </div>

            <p class="tour-step-description">{{ step.content }}</p>

            <div class="tour-navigation">
              <button
                v-if="index > 0"
                @click="() => handlePrevStep(step)"
                class="tour-button tour-button-secondary"
              >
                <ArrowLeftIcon class="w-4 h-4 mr-2" />
                Anterior
              </button>
              <button
                v-if="index < steps.length - 1"
                @click="() => handleNextStep(step)"
                class="tour-button tour-button-primary"
              >
                {{ step.nextButtonText || "Siguiente" }}
                <ArrowRightIcon class="w-4 h-4 ml-2" />
              </button>
              <button
                v-else
                @click="() => handleFinishStep(step)"
                class="tour-button tour-button-primary"
              >
                {{ step.finishButtonText || "Finalizar" }}
                <PartyPopperIcon class="w-4 h-4 ml-2" />
              </button>
            </div>
          </div>
          <div class="tour-progress-bar">
            <div
              class="tour-progress-bar-fill"
              :style="{ width: `${((currentStep + 1) / steps.length) * 100}%` }"
            ></div>
          </div>
        </div>
      </TransitionGroup>
    </div>
  </Transition>
</template>

<script setup>
import { ref, watch, onMounted, onBeforeUnmount } from "vue";
import confetti from "canvas-confetti";
import "./tourGuideStyles.css";
import {
  ArrowLeftIcon,
  ArrowRightIcon,
  PartyPopperIcon,
} from "lucide-vue-next";

const props = defineProps({
  steps: {
    type: Array,
    required: true,
    validator: (value) => {
      return value.every((step) => {
        return (
          typeof step.margin === "undefined" ||
          (typeof step.margin === "object" &&
            Object.values(step.margin).every(
              (val) =>
                typeof val === "number" ||
                typeof val === "string" ||
                typeof val === "function"
            ))
        );
      });
    },
  },
  isVisible: {
    type: Boolean,
    default: false,
  },
});

const emit = defineEmits(["end", "step-change"]);

const currentStep = ref(0);
const maskStyle = ref({});
const isWaitingForAction = ref(false);
const isStepHidden = ref(false);
const isMobile = ref(window.innerWidth < 800);
const isSmallHeight = ref(window.innerHeight < 800);

const updateScreenSize = () => {
  isMobile.value = window.innerWidth < 800;
  isSmallHeight.value = window.innerHeight < 800;
};

const updateHighlightedElement = () => {
  const step = props.steps[currentStep.value];
  if (!step || !step.id) return;

  const element = document.getElementById(step.id);
  if (element) {
    const rect = element.getBoundingClientRect();
    maskStyle.value = {
      "--highlight-top": `${rect.top}px`,
      "--highlight-left": `${rect.left}px`,
      "--highlight-width": `${rect.width}px`,
      "--highlight-height": `${rect.height}px`,
    };
  }
};

const handleResize = () => {
  updateScreenSize();
  updateHighlightedElement();
};

const getStepStyle = (step) => {
  const element = document.getElementById(step.id);
  if (!element) return {};

  const rect = element.getBoundingClientRect();
  const viewportHeight = window.innerHeight;
  const viewportWidth = window.innerWidth;

  if (isMobile.value) {
    return {
      bottom: "0",
      left: "0",
      width: "100%",
      maxWidth: "none",
    };
  } else {
    let top, left;
    const offset = 10;

    switch (step.position) {
      case "top":
        top = rect.top - 450 - offset;
        left = rect.left + rect.width / 2 - 150;
        break;
      case "bottom":
        top = rect.bottom + offset;
        left = rect.left + rect.width / 2 - 150;
        break;
      case "left":
        top = rect.top + rect.height / 2 - 100;
        left = rect.left - 310 - offset;
        break;
      case "right":
      default:
        top = rect.top + rect.height / 2 - 100;
        left = rect.right + offset;
        break;
    }

    if (top < 0) top = offset;
    if (top + 200 > viewportHeight) top = viewportHeight - 210;
    if (left < 0) left = offset;
    if (left + 300 > viewportWidth) left = viewportWidth - 310;

    // Apply custom margins if provided
    if (step.margin) {
      Object.entries(step.margin).forEach(([key, value]) => {
        if (typeof value === "function") {
          value = value({
            isSmallHeight: isSmallHeight.value,
            isMobile: isMobile.value,
          });
        }
        if (value !== undefined) {
          switch (key) {
            case "top":
              top += parseFloat(value);
              break;
            case "bottom":
              top -= parseFloat(value);
              break;
            case "left":
              left += parseFloat(value);
              break;
            case "right":
              left -= parseFloat(value);
              break;
          }
        }
      });
    }

    return {
      top: `${top}px`,
      left: `${left}px`,
    };
  }
};
function scrollToElement(selector) {
  return new Promise((resolve) => {
    const element = document.querySelector(selector);
    if (element) {
      element.scrollIntoView({
        behavior: "auto",
        block: "center",
        inline: "nearest",
      });
    }
    resolve();
  });
}

const updateMaskStyle = async () => {
  const step = props.steps[currentStep.value];
  if (!step || !step.id) return;

  await scrollToElement(`#${step.id}`);
  setTimeout(() => {
    updateHighlightedElement();
  }, 200);
};

const nextStep = async () => {
  if (currentStep.value < props.steps.length - 1) {
    currentStep.value++;
    emit("step-change", currentStep.value);
    await updateMaskStyle();
  }
};

const prevStep = async () => {
  if (currentStep.value > 0) {
    currentStep.value--;
    emit("step-change", currentStep.value);
    await updateMaskStyle();
  }
};

const handlePrevStep = async (step) => {
  if (isWaitingForAction.value) return;

  if (step.onBack) {
    isWaitingForAction.value = true;
    hideCurrentStep();
    try {
      await step.onBack();
    } catch (error) {
      console.error("Error en la acción onBack:", error);
    } finally {
      isWaitingForAction.value = false;
      showCurrentStep();
    }
  }
  await prevStep();
};

const hideCurrentStep = () => {
  isStepHidden.value = true;
};

const showCurrentStep = () => {
  isStepHidden.value = false;
};

const handleNextStep = async (step) => {
  if (isWaitingForAction.value) return;

  if (step.onNext) {
    isWaitingForAction.value = true;
    hideCurrentStep();
    try {
      await step.onNext();
    } catch (error) {
      console.error("Error en la acción onNext:", error);
    } finally {
      isWaitingForAction.value = false;
      showCurrentStep();
    }
  }
  nextStep();
};

const handleFinishStep = async (step) => {
  if (isWaitingForAction.value) return;

  isWaitingForAction.value = true;
  hideCurrentStep();

  try {
    if (step.onNext) {
      await step.onNext();
    }

    const highlightedElement = document.getElementById(step.id);
    if (highlightedElement) {
      const rect = highlightedElement.getBoundingClientRect();
      const x = (rect.left + rect.width / 2) / window.innerWidth;
      const y = (rect.top + rect.height / 2) / window.innerHeight;

      confetti({
        particleCount: 100,
        spread: 70,
        origin: { x, y },
      });
    } else {
      confetti({
        particleCount: 100,
        spread: 70,
        origin: { x: 0.5, y: 0.5 },
      });
    }

    if (step.onFinish) {
      await step.onFinish();
    }
  } catch (error) {
    console.error("Error en la acción onFinish:", error);
  } finally {
    isWaitingForAction.value = false;
    showCurrentStep();
    endTour();
  }
};

const endTour = () => {
  window.removeEventListener("scroll", updateMaskStyle);
  emit("end");
};

const handleOverlayClick = (event) => {
  if (event.target.classList.contains("tour-overlay-mask")) {
    endTour();
  }
};

watch(
  () => props.isVisible,
  (newValue) => {
    if (newValue) {
      currentStep.value = 0;
      updateMaskStyle();
      showCurrentStep();
      window.addEventListener("scroll", updateMaskStyle);
    } else {
      endTour();
    }
  }
);

watch(currentStep, updateMaskStyle);

onMounted(() => {
  updateMaskStyle();
  updateScreenSize();
  updateScreenSize();
  window.addEventListener("resize", handleResize);
  window.addEventListener("scroll", updateHighlightedElement);
});

onBeforeUnmount(() => {
  window.removeEventListener("resize", handleResize);
  window.removeEventListener("scroll", updateHighlightedElement);
});
</script>
