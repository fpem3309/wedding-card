<script setup>
defineProps({
  data: Object
});
</script>

<template>
  <div class="preview-text-container">
    <div class="preview-text-content" v-html="data.content"></div>
  </div>
</template>

<style scoped>
.preview-text-container {
  padding: 1.5rem 2rem; /* py-6 px-8 */
  background-color: white; /* bg-white */
}

.preview-text-content {
  font-size: 1rem; /* text-base */
  color: #4b5563; /* text-gray-700 */
  line-height: 1.625; /* leading-relaxed */
  text-align: center;
  /* For prose and max-w-none, we'll rely on global or parent styles,
     or add specific styles if needed for Tiptap's output */
}
</style>