<script setup>
defineProps({
  data: Object
});
</script>

<template>
  <div class="block-container">
    <h3 class="block-header">타이틀 블록</h3>
    <div class="input-group-list">
      <div class="input-group">
        <label class="input-label">신랑</label>
        <input type="text" v-model="data.groomName" class="text-input">
      </div>
      <div class="input-group">
        <label class="input-label">신부</label>
        <input type="text" v-model="data.brideName" class="text-input">
      </div>
      <div class="input-group">
        <label class="input-label">날짜</label>
        <input type="text" v-model="data.date" class="text-input">
      </div>
      <div class="input-group">
        <label class="input-label">장소</label>
        <input type="text" v-model="data.location" class="text-input">
      </div>
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

.input-group-list {
  display: flex;
  flex-direction: column;
  gap: 0.5rem; /* space-y-2 */
}

.input-group {
  /* flex-direction: column; */
}

.input-label {
  font-size: 0.75rem; /* text-xs */
  color: #4b5563; /* text-gray-600 */
  display: block; /* Ensure label takes full width */
  margin-bottom: 0.25rem; /* Small margin below label */
}

.text-input {
  width: 100%;
  padding: 0.5rem; /* p-2 */
  border: 1px solid #d1d5db; /* border border-gray-300 */
  border-radius: 0.375rem; /* rounded-md */
  outline: none; /* focus:outline-none */
  transition: all 0.2s ease; /* transition-all */
}

.text-input:focus {
  border-color: #60a5fa; /* focus:ring-blue-400 */
  box-shadow: 0 0 0 2px rgba(96, 165, 250, 0.5); /* focus:ring-2 */
}
</style>