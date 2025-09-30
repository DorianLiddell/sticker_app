<template>
  <div class="sticker">
    <img src="https://cataas.com/cat" alt="Sticker Cat" />
  </div>
</template>

<script setup lang="ts"></script>

<style scoped lang="scss">

.sticker {
  position: fixed;
  right: 20px;
  top: 50%;
  transform: translateY(-50%);
  width: 50px;
  height: 50px;
  transition: all 0.3s ease-in-out;

  img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    border-radius: 50%;
    box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);
  }

  &:hover {
    width:  50px;
    height:  50px;
    transform: translateY(-50%) scale(1.1);
  }
}
</style>