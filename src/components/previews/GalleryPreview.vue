<script setup>
defineProps({
  data: Object
});
</script>

<template>
  <div class="preview-gallery-container">
    <div class="gallery-scroll-area">
      <div v-for="(imageUrl, index) in data.images" :key="index" class="gallery-item">
        <img :src="imageUrl" class="gallery-image" alt="Gallery image">
      </div>
    </div>
  </div>
</template>

<style scoped>
.preview-gallery-container {
  padding-top: 1.5rem; /* py-6 */
  padding-bottom: 1.5rem;
  background-color: white; /* bg-white */
}

.gallery-scroll-area {
  display: flex;
  overflow-x: auto;
  gap: 1rem; /* space-x-4 */
  padding: 1rem; /* p-4 */
}

.gallery-item {
  flex-shrink: 0;
}

.gallery-image {
  width: 16rem; /* w-64 */
  height: 12rem; /* h-48 */
  object-fit: cover;
  border-radius: 0.5rem; /* rounded-lg */
  box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -2px rgba(0, 0, 0, 0.06); /* shadow-md */
  border: 1px solid #e5e7eb; /* border border-gray-200 */
}
</style>