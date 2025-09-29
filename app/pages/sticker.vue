<template>
  <div class="container">
    <div class="content">
      <p v-for="i in 20" :key="i">Это длинный контент для скроллинга. Пункт {{ i }}.</p>
      <img v-for="(image, index) in catImages" :key="index" :src="image.url" alt="Cat" class="cat-image" />
    </div>
    <Sticker />
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, onMounted } from 'vue';
import Sticker from '~/components/Sticker.vue';
import axios from 'axios';

export default defineComponent({
  name: 'StickerPage',
  components: { Sticker },
  setup() {
    const catImages = ref<Array<{ url: string }>>([]);

    const fetchCatImage = async (index: number) => {
      try {
        const response = await axios.get('https://cataas.com/cat', { responseType: 'blob' });
        const url = URL.createObjectURL(response.data);
        catImages.value[index] = { url };
      } catch (error) {
        console.error('Error fetching cat image:', error);
      }
    };

    onMounted(async () => {
      for (let i = 0; i < 3; i++) {
        catImages.value.push({ url: '' });
        await fetchCatImage(i);
      }
    });

    return { catImages };
  },
});
</script>

<style scoped lang="scss">
.container {
  min-height: 100vh;
  padding: 20px;
}

.content {
  height: 800px; 
  overflow-y: auto;
  margin-bottom: 20px;
}

.cat-image {
  width: 200px;
  height: 200px;
  object-fit: cover;
  margin: 10px 0;
}

p {
  margin: 10px 0;
  line-height: 1.5;
}
</style>