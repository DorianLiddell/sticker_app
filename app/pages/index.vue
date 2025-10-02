<template>
  <div class="app-container">
    <Sidebar @toggle="handleToggle" />
    <div class="sticker-page">
      <div v-if="isContentVisible" class="content-wrapper">
        <h1>Консультация эксперта</h1>
        <div class="content">
          <div v-if="isLoading" class="loader">Загрузка...</div>
          <div v-if="error" class="error-message">Ошибка загрузки</div>
          <div v-for="cat in cats" :key="cat.id" class="cat-card" v-else>
            <img :src="cat.url" alt="Cat image" @error="handleImageError" />
          </div>
        </div>
        <NuxtLink to="/sticker" class="sticker-button">Перейти к странице стикера</NuxtLink>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import type { Cat } from '~/types/index'; 
import Sidebar from '~/components/Sidebar.vue';

definePageMeta({
  layout: 'default',
});

const cats = ref<Cat[]>([]);
const isContentVisible = ref(false);
const isLoading = ref(true); 
const error = ref(false); 

const fetchCats = async () => {
  try {
    isLoading.value = true; 
    error.value = false; 
    const response1 = await $fetch('https://cataas.com/cat', { responseType: 'blob' }) as Blob;
    const response2 = await $fetch('https://cataas.com/cat', { responseType: 'blob' }) as Blob;
    const response3 = await $fetch('https://cataas.com/cat', { responseType: 'blob' }) as Blob;

    cats.value = [
      { id: 1, url: URL.createObjectURL(response1) },
      { id: 2, url: URL.createObjectURL(response2) },
      { id: 3, url: URL.createObjectURL(response3) },
    ];
  } catch (err) {
    error.value = true; 
    console.error('Ошибка при загрузке:', err);
  } finally {
    isLoading.value = false; 
  }
};

const handleImageError = () => {
  error.value = true; 
};

const handleToggle = (expanded: boolean) => {
  isContentVisible.value = expanded; 
  if (expanded && cats.value.length === 0) {
    fetchCats();
  }
};

fetchCats();
</script>

<style scoped lang="scss">

@font-face {
  font-family: 'Exo 2';
  src: url('~/assets/fonts/Exo2-SemiBold.ttf') format('truetype');
  font-weight: 400;
  font-style: normal;
}

@font-face {
  font-family: 'Exo 2';
  src: url('~/assets/fonts/Exo2-Medium.ttf') format('truetype');
  font-weight: 400;
  font-style: medium;
}

.app-container {
  display: flex;
  min-height: 100vh; 
  position: relative; 
  width: 100%;
  align-items: flex-start; 
}

.sticker-page {
  padding: 10px;
  margin: 0; 
  display: flex;
  flex-direction: column;
  align-items: flex-start; 
  justify-content: center; 
  min-height: 100vh;
  flex-grow: 1; 

  .content-wrapper {
    width: 320px;
    height: 320px;
    border-radius: 8px;
    transition: opacity 0.5s ease; 
    opacity: 1;
    margin-left: 0; 
    background: #F4F6F9;
    display: flex;
    flex-direction: column;
    align-items: center; 
    justify-content: center;

    &.hidden {
      opacity: 0;
      pointer-events: none;
    }

    h1 {
    font-family: 'Exo 2';
    font-weight: 600;
    font-size: 23px;
    font-style: normal;
    color: #333;
    margin: 0 0 20px 0;
    text-align: center;
    white-space: normal; 
    max-width: 200px; 
    }
  }

  .content {
    display: flex;
    flex-wrap: wrap;
    justify-content: center; 

    .cat-card {
      margin-left: -10px;
      width: 64px;
      height: 64px;
      background: white;
      border-radius: 16px;
      text-align: center;

      img {
        width: 64px;
        height: 64px;
        border-radius: 16px;
        object-fit: cover;
        border: 3px solid #F4F6F9;
      }

      p {
        margin-top: 10px;
        font-size: 1.2rem;
        color: #333;
      }
    }

  .loader {
      font-family: 'Exo 2', sans-serif;
      font-weight: 500;
      font-size: 16px;
      color: #666;
      text-align: center;
      padding: 10px;
    }

    .error-message {
      font-family: 'Exo 2', sans-serif;
      font-weight: 500;
      font-size: 16px;
      color: #d32f2f; 
      text-align: center;
      padding: 10px;
    }
  }

  .sticker-button {
    font-family: 'Exo 2';
    font-weight: 500;
    font-style: medium;
    font-size: 16px;
    width: 232px;
    height: 40px;
    color: #000;
    background-color: white;
    display: flex; 
    align-items: center; 
    justify-content: center; 
    text-decoration: none;
    padding: 10px 20px;
    border-radius: 5px;
    margin-top: 30px;
    text-align: center;
    transition: background-color 0.5s;

    &:hover {
        background-color: #bfc0c2;
      }
  }
}
</style>


