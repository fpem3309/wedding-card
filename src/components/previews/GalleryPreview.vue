<script setup>
import { Swiper, SwiperSlide } from 'swiper/vue'; // Import Swiper components
import { Pagination, Navigation } from 'swiper/modules'; // Import Swiper modules

// Import Swiper styles
import 'swiper/css';
import 'swiper/css/pagination';
import 'swiper/css/navigation';

defineProps({
  data: Object
});
</script>

<template>
  <div class="preview-gallery-container">
    <swiper
      :modules="[Pagination, Navigation]"
      :slides-per-view="1"
      :space-between="10"
      navigation
      :pagination="{ clickable: true }"
      class="mySwiper"
    >
      <swiper-slide v-for="(imageUrl, index) in data.images" :key="index">
        <div class="gallery-item"> <!-- Keep this for styling individual images -->
          <img :src="imageUrl" class="gallery-image" alt="Gallery image">
        </div>
      </swiper-slide>
    </swiper>
  </div>
</template>

<style scoped>
.preview-gallery-container {
  padding-top: 1.5rem; /* py-6 */
  padding-bottom: 1.5rem;
  background-color: white; /* bg-white */
}

/* Remove .gallery-scroll-area CSS */
/*
.gallery-scroll-area {
  display: flex;
  overflow-x: auto;
  gap: 1rem;
  padding: 1rem;
}
*/

.mySwiper {
  width: 20rem; /* Now 100% of max-width: 300px */
  height: 8rem; /* Keep height at 8rem */
  margin-bottom: 0.5rem;
  padding: 1rem; /* Add padding to the swiper container */
  box-sizing: border-box; /* Ensure padding is included in width */
  overflow: hidden; /* Explicitly hide overflow */
}

.swiper-slide {
  width: 100%;
  height: auto; /* Allow slide height to adjust */
}

.gallery-item {
  flex-shrink: 0;
  width: 100%; /* Ensure it takes full width of slide */
  height: 100%; /* Ensure it takes full height of slide */
  display: flex; /* Added for centering image */
  align-items: center; /* Added for centering image */
  justify-content: center; /* Added for centering image */
}

.gallery-image {
  width: 100%; /* w-64 */
  height: auto; /* Set height to auto to maintain aspect ratio */
  max-height: 10rem; /* Set a max-height to prevent excessively tall images */
  object-fit: contain; /* Changed from cover to contain */
  border-radius: 0.5rem; /* rounded-lg */
  box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -2px rgba(0, 0, 0, 0.06); /* shadow-md */
  border: 1px solid #e5e7eb; /* border border-gray-200 */
}
</style>