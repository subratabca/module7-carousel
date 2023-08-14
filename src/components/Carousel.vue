<template>
  <div class="carousel">
    <div class="slide-container">
      <transition name="fade" mode="out-in">
        <img :key="currentIndex" :src="currentImage" class="slide" />
      </transition>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue';

const images = [
    'https://images.unsplash.com/photo-1684220054800-a40a9f7e8f96?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1174&q=80',
    'https://images.unsplash.com/photo-1691351942772-cafcf9c37474?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1170&q=80',
    'https://images.unsplash.com/photo-1691059283093-1e4345a9fa71?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1171&q=80'
];

const currentIndex = ref(0);

const currentImage = ref(images[currentIndex.value]);

const updateImage = () => {
  currentImage.value = images[currentIndex.value];
};

const nextSlide = () => {
  currentIndex.value = (currentIndex.value + 1) % images.length;
  updateImage();
};

const prevSlide = () => {
  currentIndex.value = (currentIndex.value - 1 + images.length) % images.length;
  updateImage();
};

onMounted(() => {
  const interval = setInterval(nextSlide, 3000);
  updateImage();

  onBeforeUnmount(() => {
    clearInterval(interval);
  });
});
</script>

<style scoped>
.carousel {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

.slide-container {
  position: relative;
  width: 100%;
  max-width: 800px;
  overflow: hidden;
}

.slide {
  width: 100%;
  height: auto;
  object-fit: cover;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 1s;
}

.fade-enter,
.fade-leave-to {
  opacity: 0;
}
</style>
