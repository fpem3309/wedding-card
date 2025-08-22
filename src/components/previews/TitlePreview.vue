<script setup>
defineProps({
  data: Object
});
</script>

<template>
  <div class="preview-title-container">
    <h1 class="preview-title">{{ data.groomName }} <span class="heart-icon">♥</span> {{ data.brideName }}</h1>
    <p class="preview-date">{{ data.date }}</p>
    <p class="preview-location">{{ data.location }}</p>
  </div>
</template>

<style scoped>
.preview-title-container {
  text-align: center;
  padding: 2rem 1rem; /* py-8 px-4 */
  background-color: white; /* bg-white */
}

.preview-title {
  font-size: 2.25rem; /* text-4xl */
  font-family: serif; /* font-serif */
  color: #1f2937; /* text-gray-800 */
  line-height: 1.25; /* leading-tight */
  margin-bottom: 0.5rem; /* mb-2 */
}

.heart-icon {
  color: #ec4899; /* text-pink-500 */
}

.preview-date {
  margin-top: 1rem; /* mt-4 */
  font-size: 1.125rem; /* text-lg */
  color: #4b5563; /* text-gray-600 */
  font-weight: 500; /* font-medium */
}

.preview-location {
  margin-top: 0.5rem; /* mt-2 */
  font-size: 1.125rem; /* text-lg */
  color: #4b5563; /* text-gray-600 */
}
</style>