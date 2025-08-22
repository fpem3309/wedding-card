<script setup>
import { ref } from 'vue';

const props = defineProps({
  data: Object
});

const fileInput = ref(null);

function triggerFileInput() {
  fileInput.value.click();
}

function handleFileUpload(event) {
  const file = event.target.files[0];
  if (!file) return;

  const reader = new FileReader();
  reader.onload = (e) => {
    props.data.src = e.target.result;
  };
  reader.readAsDataURL(file);
  event.target.value = '';
}
</script>

<template>
  <div class="block-container">
    <h3 class="block-header">이미지 블록</h3>
    <input type="file" ref="fileInput" @change="handleFileUpload" accept="image/*" class="file-input-hidden">
    
    <div v-if="data.src" class="image-display">
      <img :src="data.src" class="image-thumbnail" alt="Image">
    </div>

    <button @click="triggerFileInput" class="add-image-button">
      {{ data.src ? '이미지 변경' : '+ 이미지 선택' }}
    </button>

    <div class="caption-input-group">
      <label class="input-label">캡션 (선택 사항)</label>
      <input type="text" v-model="data.caption" class="text-input" placeholder="사진에 대한 설명을 입력하세요...">
    </div>
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

.image-display {
  margin-bottom: 0.5rem; /* mb-2 */
  border: 1px solid #e5e7eb; /* border border-gray-200 */
  border-radius: 0.375rem; /* rounded-md */
  overflow: hidden;
  display: flex;
  align-items: center;
  justify-content: center;
}

.image-thumbnail {
  width: 100%;
  height: auto;
  max-height: 16rem; /* max-h-64 */
  object-fit: contain;
  background-color: #f3f4f6; /* bg-gray-100 */
}

.add-image-button {
  width: 100%;
  font-size: 0.875rem; /* text-sm */
  background-color: #f3f4f6; /* bg-gray-100 */
  color: #4b5563; /* text-gray-700 */
  padding: 0.5rem 0.75rem; /* py-2 px-3 */
  border-radius: 0.375rem; /* rounded-md */
  border: 1px solid #d1d5db; /* border border-gray-300 */
  transition: background-color 0.2s ease;
}

.add-image-button:hover {
  background-color: #e5e7eb; /* hover:bg-gray-200 */
}

.caption-input-group {
  margin-top: 0.5rem; /* mt-2 */
}

.input-label {
  font-size: 0.75rem; /* text-xs */
  color: #4b5563; /* text-gray-600 */
  display: block;
  margin-bottom: 0.25rem;
}

.text-input {
  width: 100%;
  font-size: 0.875rem; /* text-sm */
  padding: 0.5rem; /* p-2 */
  border: 1px solid #d1d5db; /* border border-gray-300 */
  border-radius: 0.375rem; /* rounded-md */
  outline: none; /* focus:outline-none */
  transition: all 0.2s ease;
}

.text-input:focus {
  border-color: #60a5fa; /* focus:ring-blue-400 */
  box-shadow: 0 0 0 2px rgba(96, 165, 250, 0.5); /* focus:ring-2 */
}
</style>