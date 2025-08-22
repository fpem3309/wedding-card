<script setup>
import { ref } from 'vue';
import draggable from 'vuedraggable';

const props = defineProps({
  data: Object
});

const fileInput = ref(null);

function triggerFileInput() {
  fileInput.value.click();
}

function handleFileUpload(event) {
  const files = event.target.files;
  if (!files) return;

  for (const file of files) {
    const reader = new FileReader();
    reader.onload = (e) => {
      if (!props.data.images) {
        props.data.images = [];
      }
      props.data.images.push(e.target.result);
    };
    reader.readAsDataURL(file);
  }
  // Clear the input value to allow uploading the same file again
  event.target.value = '';
}

function removeImage(index) {
  props.data.images.splice(index, 1);
}
</script>

<template>
  <div class="block-container">
    <h3 class="block-header">갤러리 블록</h3>
    
    <input type="file" ref="fileInput" @change="handleFileUpload" multiple accept="image/*" class="file-input-hidden">

    <draggable
      v-if="data.images && data.images.length"
      :list="data.images"
      item-key="index"
      class="image-grid"
    >
      <template #item="{ element: imageUrl, index }">
        <div class="image-grid-item">
          <img :src="imageUrl" class="image-thumbnail" alt="Gallery image">
          <button @click="removeImage(index)" class="remove-image-button">
            X
          </button>
        </div>
      </template>
    </draggable>
    <div v-else class="no-image-placeholder">
      이미지를 추가해주세요.
    </div>

    <button @click="triggerFileInput" class="add-image-button">
      + 컴퓨터에서 이미지 선택...
    </button>
  </div>
</template>

<style scoped>
.block-container {
  padding: 1rem; /* p-4 */
  background-color: white; /* bg-white */
  border-radius: 0.5rem; /* rounded-lg */
  box-shadow: 0 1px 2px 0 rgba(0, 0, 0, 0.05); /* shadow-sm */
  border: 1px solid #e5e7eb; /* border border-gray-200 */
}

.block-header {
  font-size: 0.875rem; /* text-sm */
  font-weight: 600; /* font-semibold */
  color: #6b7280; /* text-gray-500 */
  margin-bottom: 0.75rem; /* mb-3 */
}

.file-input-hidden {
  display: none;
}

.image-grid {
  display: grid;
  grid-template-columns: repeat(3, minmax(0, 1fr)); /* grid-cols-3 */
  gap: 0.5rem; /* gap-2 */
  margin-bottom: 0.5rem; /* mb-2 */
}

.image-grid-item {
  position: relative;
  border: 1px solid #e5e7eb; /* border border-gray-200 */
  border-radius: 0.375rem; /* rounded-md */
  overflow: hidden;
  display: flex;
  align-items: center;
  justify-content: center;
}

.image-thumbnail {
  width: 100%;
  height: 6rem; /* h-24 */
  object-fit: cover;
}

.remove-image-button {
  position: absolute;
  top: 0.5rem; /* Adjusted to match delete-button */
  right: 0.5rem; /* Adjusted to match delete-button */
  background-color: #f8d7da; /* Very light red/pink */
  color: #721c24; /* Darker red for text */
  border-radius: 9999px; /* rounded-full */
  width: 1.75rem; /* w-7, Adjusted to match delete-button */
  height: 1.75rem; /* h-7, Adjusted to match delete-button */
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 0.875rem; /* text-sm, Adjusted to match delete-button */
  opacity: 1; /* Always visible */
  transition: opacity 0.3s ease, transform 0.3s ease;
}

.image-grid-item:hover .remove-image-button {
  transform: scale(1.1);
  background-color: #f5c6cb; /* Darker on hover */
  color: #721c24; /* Keep text color consistent */
}
.no-image-placeholder {
  text-align: center;
  font-size: 0.875rem; /* text-sm */
  color: #6b7280; /* text-gray-500 */
  padding-top: 2rem; /* py-8 */
  padding-bottom: 2rem;
  background-color: white; /* bg-white */
  border-radius: 0.375rem; /* rounded-md */
}

.add-image-button {
  width: 100%;
  font-size: 0.875rem; /* text-sm */
  background-color: #f3f4f6; /* bg-gray-100 */
  color: #4b5563; /* text-gray-700 */
  padding-top: 0.5rem; /* py-2 */
  padding-bottom: 0.5rem;
  padding-left: 0.75rem; /* px-3 */
  padding-right: 0.75rem;
  border-radius: 0.375rem; /* rounded-md */
  margin-top: 0.5rem; /* mt-2 */
  border: 1px solid #d1d5db; /* border border-gray-300 */
  transition: background-color 0.2s ease;
}

.add-image-button:hover {
  background-color: #e5e7eb; /* hover:bg-gray-200 */
}
</style>