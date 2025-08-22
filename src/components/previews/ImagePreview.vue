<script setup>
defineProps({
  data: Object
});
</script>

<template>
  <div class="preview-image-container">
    <figure v-if="data.src" class="image-figure">
      <img :src="data.src" class="image-display" alt="Image">
      <figcaption v-if="data.caption" class="image-caption">
        {{ data.caption }}
      </figcaption>
    </figure>
  </div>
</template>

<style scoped>
.preview-image-container {
  padding: 2rem 1rem; /* py-8 px-4 */
  text-align: center;
  background-color: white; /* bg-white */
}

.image-figure {
  /* flex-direction: column; */
}

.image-display {
  width: 100%;
  height: auto;
  border-radius: 0.5rem; /* rounded-lg */
  box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -2px rgba(0, 0, 0, 0.06); /* shadow-lg */
  margin-left: auto; /* mx-auto */
  margin-right: auto; /* mx-auto */
  border: 1px solid #e5e7eb; /* border border-gray-200 */
}

.image-caption {
  margin-top: 0.75rem; /* mt-3 */
  font-size: 0.875rem; /* text-sm */
  color: #4b5563; /* text-gray-600 */
  font-style: italic;
  font-weight: 500; /* font-medium */
}
</style>