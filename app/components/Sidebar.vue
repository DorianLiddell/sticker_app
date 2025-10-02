<template>
  <div class="sidebar" :class="{ 'expanded': isExpanded }" @click="toggleSidebar">
    <div v-for="index in 3" :key="index" class="profile">
      <img src="https://cataas.com/cat" alt="Sticker Cat" />
    </div>
    <img v-if="!isExpanded" src="~/assets/images/arrow-right.png" alt="Expand Arrow" class="arrow" />
    <img v-else src="~/assets/images/arrow-left.png" alt="Collapse Arrow" class="arrow" />
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';

const emit = defineEmits(['toggle']);
const isExpanded = ref(false);

const toggleSidebar = () => {
  isExpanded.value = !isExpanded.value;
  emit('toggle', isExpanded.value);
};
</script>

<style scoped lang="scss">
.sidebar {
  position: fixed; 
  right: 14px; 
  top: 50%; 
  margin-top: -133px; 
  width: 80px;
  height: 266px;
  background: #F4F6F9;
  border-radius: 10px 0 0 10px; 
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 22px 0;

  .profile {
    margin-top: -10px;
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
  }

  .arrow {
    width: 24px; 
    height: 24px;
    object-fit: contain;
    cursor: pointer;
    margin-top: 52px;
  }
}
</style>