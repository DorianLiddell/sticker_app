<template>
  <div class="container">
    <NuxtLink to="/">Вернуться на главную</NuxtLink>

    <section class="hero">
      <p>Это пример страницы с различными блоками контента, чтобы обеспечить прокрутку.</p>
    </section>

    <section class="cards">
      <div class="card" v-for="item in 8" :key="item">
        <h2>Карточка {{ item }}</h2>
        <p>Это пример карточки с текстом.</p>
        <button>Подробнее</button>
      </div>
    </section>

    <section class="text-content">
      <h2>О нас</h2>
      <p v-for="i in 5" :key="i">
        Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor incididunt ut
        labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco
        laboris nisi ut aliquip ex ea commodo consequat.
      </p>
    </section>

    <footer class="footer">
      <p>© 2025 Моя страница. Все права защищены.</p>
    </footer>
  </div>
</template>

<script setup lang="ts">
definePageMeta({
  layout: 'default',
});
</script>

<style scoped lang="scss">

@font-face {
  font-family: 'Exo 2';
  src: url('~/assets/fonts/Exo2-Regular.ttf') format('truetype');
  font-weight: 400;
  font-style: normal;
}

.container {
  font-family: 'Exo 2';
  font-weight: 400;
  font-style: normal;
  text-align: center;
  padding: 50px 20px;
  display: flex;
  flex-direction: column;
  align-items: center;
  min-height: 100vh; 
}

a {
  font-size: 18px;
  padding: 10px 20px;
  border-radius: 5px;
  text-decoration: none;
  background-color: #3f3f3f;
  color: white;
  transition: background-color 0.3s;
  margin-bottom: 40px;

  &:hover {
    background-color: #bfc0c2;
  }
}

.hero {
  margin-bottom: 60px;


  p {
    font-size: 18px;
    color: #555;
    max-width: 600px;
  }
}

.cards {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 20px;
  margin-bottom: 60px;
  width: 100%;
  max-width: 1200px;

  .card {
    background-color: #f9f9f9;
    padding: 20px;
    border-radius: 10px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    transition: transform 0.3s;

    &:hover {
      transform: translateY(-5px);
    }

    h2 {
      font-size: 24px;
      margin-bottom: 10px;
    }

    p {
      font-size: 16px;
      color: #666;
      margin-bottom: 15px;
    }

    button {
      padding: 10px 20px;
      border: none;
      border-radius: 5px;
      background-color: #3f3f3f;
      color: white;
      cursor: pointer;
      transition: background-color 0.3s;

      &:hover {
        background-color: #bfc0c2;
      }
    }
  }
}

.text-content {
  margin-bottom: 60px;
  max-width: 800px;

  h2 {
    font-size: 28px;
    margin-bottom: 20px;
  }

  p {
    font-size: 16px;
    color: #444;
    line-height: 1.6;
    margin-bottom: 15px;
  }
}

.footer {
  padding: 20px;
  background-color: #f1f1f1;
  width: 100%;
  text-align: center;

  p {
    font-size: 14px;
    color: #777;
  }
}
</style>