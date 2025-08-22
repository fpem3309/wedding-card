<script setup>
// This block doesn't need specific editing UI, as its content is derived.
// It will just display the calculated D-Day.
</script>

<template>
  <div class="block-container">
    <h3 class="block-header">D-Day 블록</h3>
    <p class="info-text">미리보기에서 D-Day가 자동으로 계산되어 표시됩니다.</p>
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

.info-text {
  text-align: center;
  color: #4b5563; /* text-gray-600 */
  font-size: 0.875rem; /* text-sm */
}
</style>