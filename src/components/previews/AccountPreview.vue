<script setup>
import { ref } from 'vue';

defineProps({
  data: Object
});

const copiedIndex = ref(null);

async function copyToClipboard(text, index) {
  try {
    await navigator.clipboard.writeText(text);
    copiedIndex.value = index;
    setTimeout(() => {
      copiedIndex.value = null;
    }, 2000); // Reset after 2 seconds
  } catch (err) {
    console.error('Failed to copy: ', err);
    alert('클립보드 복사에 실패했습니다.');
  }
}
</script>

<template>
  <div class="preview-account-container">
    <h2 class="preview-account-header">마음 전하실 곳</h2>
    <div v-if="data.accounts && data.accounts.length" class="account-list">
      <div v-for="(account, index) in data.accounts" :key="index" class="account-item">
        <div class="account-details">
          <p class="account-bank">{{ account.bank }}</p>
          <p class="account-number">{{ account.number }}</p>
          <p class="account-name">{{ account.name }}</p>
        </div>
        <button @click="copyToClipboard(account.number, index)" class="copy-button">
          {{ copiedIndex === index ? '복사됨!' : '복사' }}
        </button>
      </div>
    </div>
  </div>
</template>

<style scoped>
.preview-account-container {
  padding: 1.5rem 1rem; /* py-6 px-4 */
  text-align: center;
  background-color: white; /* bg-white */
}

.preview-account-header {
  font-size: 1.25rem; /* text-xl */
  font-family: serif; /* font-serif */
  margin-bottom: 1rem; /* mb-4 */
  color: #1f2937; /* text-gray-800 */
}

.account-list {
  display: flex;
  flex-direction: column;
  gap: 0.75rem; /* space-y-3 */
  max-width: 12rem; /* max-w-xs */
  margin-left: auto; /* mx-auto */
  margin-right: auto; /* mx-auto */
}

.account-item {
  padding: 0.75rem; /* p-3 */
  background-color: #f3f4f6; /* bg-gray-100 */
  border-radius: 0.5rem; /* rounded-lg */
  text-align: left;
  border: 1px solid #e5e7eb; /* border border-gray-200 */
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.account-details {
  /* flex-direction: column; */
}

.account-bank {
  font-weight: 600; /* font-semibold */
  color: #4b5563; /* text-gray-700 */
}

.account-number {
  font-size: 0.875rem; /* text-sm */
  color: #4b5563; /* text-gray-600 */
}

.account-name {
  font-size: 0.875rem; /* text-sm */
  color: #6b7280; /* text-gray-500 */
}

.copy-button {
  font-size: 0.875rem; /* text-sm */
  padding: 0.25rem 0.75rem; /* px-3 py-1 */
  border-radius: 9999px; /* rounded-full */
  background-color: #3b82f6; /* bg-blue-500 */
  color: white;
  transition: all 0.2s ease; /* transition */
  box-shadow: 0 1px 2px 0 rgba(0, 0, 0, 0.05); /* shadow-sm */
}

.copy-button:hover {
  background-color: #2563eb; /* hover:bg-blue-600 */
}
</style>