<!-- pages/index.vue -->
<template>
  <div class="sticker-page">
    <div class="content">
      <div v-for="cat in cats" :key="cat.id" class="cat-card">
        <img :src="cat.url" alt="Cat image" />
        <p>Котик №{{ cat.id }}</p>
      </div>
      <NuxtLink to="/sticker">Перейти к другой странице</NuxtLink>
    </div>
    <Sticker />
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import type { Cat } from '~/types/index';

definePageMeta({
  layout: 'default',
});

const cats = ref<Cat[]>([]);

const fetchCats = async () => {
  try {
    const response1 = await $fetch('https://cataas.com/cat', { responseType: 'blob' }) as Blob;
    const response2 = await $fetch('https://cataas.com/cat', { responseType: 'blob' }) as Blob;
    const response3 = await $fetch('https://cataas.com/cat', { responseType: 'blob' }) as Blob;

    cats.value = [
      { id: 1, url: URL.createObjectURL(response1) },
      { id: 2, url: URL.createObjectURL(response2) },
      { id: 3, url: URL.createObjectURL(response3) },
    ];
  } catch (error) {
    console.error('Ошибка при загрузке:', error);
  }
};

fetchCats();
</script>

<style scoped lang="scss">

.sticker-page {
  padding: 20px;
  max-width: 1200px;
  margin: 0 auto;

  a {
    display: inline-block;
    text-decoration: none;
    padding: 10px 20px;
    border-radius: 5px;
    margin-bottom: 20px;
    text-align: center;
    transition: background-color 0.3s;
  }

  .content {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 20px;

    .cat-card {
      background: white;
      border-radius: 10px;
      padding: 20px;
      box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
      text-align: center;

      img {
        max-width: 100%;
        border-radius: 10px;
        height: 200px;
        object-fit: cover;
      }

      p {
        margin-top: 10px;
        font-size: 1.2rem;
        color: #333;
      }
    }
  }
}
</style>