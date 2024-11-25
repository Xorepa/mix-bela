<template>
  <q-page padding>
    <div class="row q-col-gutter-md">
      <div v-for="item in items" :key="item.id" class="col-12 col-sm-6 col-md-4">
        <q-card class="cursor-pointer" @click="openCarousel(item)">
          <q-img
            :src="getImageUrl(`${item.id}-1.jpg`)"
            :ratio="1"
            style="height: 300px"
          >
            <template v-slot:error>
              <div class="absolute-full flex flex-center text-negative">
                <q-icon name="error" size="2em" />
                Imagem não encontrada
              </div>
            </template>
          </q-img>
          <q-card-section>
            <div class="text-h6">Item {{ item.id }}</div>
          </q-card-section>
        </q-card>
      </div>
    </div>

    <!-- Carrossel Modal -->
    <q-dialog v-model="showCarousel" full-width>
      <q-card>
        <q-carousel
          v-model="slide"
          animated
          arrows
          navigation
          infinite
          height="70vh"
        >
          <q-carousel-slide
            v-for="(image, index) in selectedItem.images"
            :key="index"
            :name="index"
          >
            <q-img
              :src="image"
              style="height: 100%"
              fit="contain"
            >
              <template v-slot:error>
                <div class="absolute-full flex flex-center text-negative">
                  <q-icon name="error" size="2em" />
                  Imagem não encontrada
                </div>
              </template>
            </q-img>
          </q-carousel-slide>
        </q-carousel>

        <q-card-actions align="right">
          <q-btn flat label="Fechar" color="primary" v-close-popup />
        </q-card-actions>
      </q-card>
    </q-dialog>
  </q-page>
</template>

<script setup lang="ts">
import { ref } from 'vue';

// Função para obter URL das imagens
const getImageUrl = (name: string) => {
  return new URL(`../assets/images/${name}`, import.meta.url).href;
};

interface Item {
  id: number;
  images: string[];
}

// Configuração dos itens com suas respectivas imagens
const items = ref<Item[]>([
  {
    id: 1,
    images: [
      getImageUrl('1-1.jpg'),
      getImageUrl('1-2.jpg'),
      getImageUrl('1-3.jpg')
    ]
  },
  {
    id: 2,
    images: [
      getImageUrl('2-1.jpg'),
      getImageUrl('2-2.jpg')
    ]
  },
  {
    id: 3,
    images: [
      getImageUrl('3-1.jpg'),
      getImageUrl('3-2.jpg')
    ]
  },
  // Adicione mais itens conforme necessário
]);

const showCarousel = ref(false);
const selectedItem = ref<Item>({ id: 0, images: [] });
const slide = ref(0);

function openCarousel(item: Item) {
  selectedItem.value = item;
  slide.value = 0;
  showCarousel.value = true;
}
</script>

<style scoped>
.q-img {
  transition: transform 0.3s;
}

.q-card:hover .q-img {
  transform: scale(1.05);
}
</style>
