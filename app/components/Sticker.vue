<template>
  <div class="sticker-container">
    <div class="sticker" @mouseover="expand" @mouseleave="collapse">
      <img :src="imageUrl" alt="Cat Sticker" class="sticker-img" />
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';

export default defineComponent({
  name: 'Sticker',
  setup() {
    const imageUrl = ref('/images/cat1.jpg'); 
    const isExpanded = ref(false);

    const expand = () => {
      isExpanded.value = true;
    };

    const collapse = () => {
      isExpanded.value = false;
    };

    return { imageUrl, expand, collapse };
  },
});
</script>

<style scoped lang="scss">
.sticker-container {
  position: fixed;
  right: 20px;
  top: 50%;
  transform: translateY(-50%);
  z-index: 1000;
}

.sticker {
  width: 50px;
  height: 50px;
  overflow: hidden;
  transition: width 0.3s ease, height 0.3s ease;

  &.expanded {
    width: 100px;
    height: 100px;
  }

  &:hover {
    &.expanded {
      width: 100px;
      height: 100px;
    }
  }
}

.sticker-img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}
</style>