<template>
  <q-dialog
    :model-value="modelValue"
    @update:model-value="$emit('update:modelValue', $event)"
    full-width
    maximized
    seamless
    @click-outside="$emit('update:modelValue', false)"
  >
    <div class="carousel-wrapper">
      <!-- Imagem atual -->
      <div class="image-container">
        <q-img
          :src="images[currentIndex]"
          class="carousel-image"
          fit="contain"
        >
          <template v-slot:error>
            <div class="absolute-full flex flex-center text-negative">
              <q-icon name="error" size="2em" />
              Imagem não encontrada
            </div>
          </template>
        </q-img>
      </div>

      <!-- Setas de navegação -->
      <q-btn
        round
        color="dark"
        icon="chevron_left"
        class="arrow-btn left-arrow"
        @click="previousImage"
        v-if="images.length > 1"
      />
      <q-btn
        round
        color="dark"
        icon="chevron_right"
        class="arrow-btn right-arrow"
        @click="nextImage"
        v-if="images.length > 1"
      />

      <!-- Botão de fechar -->
      <q-btn
        round
        color="dark"
        icon="close"
        class="close-btn"
        @click="$emit('update:modelValue', false)"
      />
    </div>
  </q-dialog>
</template>

<script setup lang="ts">
import { ref, watch } from 'vue';

const props = defineProps<{
  modelValue: boolean;
  images: string[];
}>();

defineEmits<{
  'update:modelValue': [value: boolean]
}>();

const currentIndex = ref(0);

watch(() => props.modelValue, (newValue) => {
  if (newValue) {
    currentIndex.value = 0;
  }
});

function nextImage() {
  currentIndex.value = (currentIndex.value + 1) % props.images.length;
}

function previousImage() {
  currentIndex.value = currentIndex.value === 0
    ? props.images.length - 1
    : currentIndex.value - 1;
}
</script>

<style scoped>
.carousel-wrapper {
  position: relative;
  width: 100%;
  height: 100vh;
  background: rgba(0, 0, 0, 0.9);
  display: flex;
  align-items: center;
  justify-content: center;
}

.image-container {
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 40px;
}

.carousel-image {
  max-height: 100%;
  width: 100%;
  object-fit: contain;
}

.arrow-btn {
  position: fixed;
  top: 50%;
  transform: translateY(-50%);
  z-index: 5000;
  opacity: 0.7;
  transition: opacity 0.3s;
}

.arrow-btn:hover {
  opacity: 1;
}

.left-arrow {
  left: 20px;
}

.right-arrow {
  right: 20px;
}

.close-btn {
  position: fixed;
  top: 20px;
  right: 20px;
  z-index: 5000;
  opacity: 0.7;
  transition: opacity 0.3s;
}

.close-btn:hover {
  opacity: 1;
}
</style>
