<template>
  <div class="container">
    <a href="/sticker">Перейти на страницу стикера</a>
  </div>
</template>

<script lang="ts">
export default {
  name: 'HomePage',
};
</script>

<style scoped lang="scss">
.container {
  text-align: center;
  padding-top: 50px;
}

a {
  font-size: 18px;
  padding: 10px 20px;
  background-color: #007bff;
  color: white;
  border-radius: 5px;
  &:hover {
    background-color: #0056b3;
  }
}
</style>