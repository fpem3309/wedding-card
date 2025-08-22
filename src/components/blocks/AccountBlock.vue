<script setup>
const props = defineProps({
  data: Object
});

// Initialize accounts array if it doesn't exist
if (!props.data.accounts) {
  props.data.accounts = [];
}

function addAccount() {
  props.data.accounts.push({ bank: '', number: '', name: '' });
}

function removeAccount(index) {
  props.data.accounts.splice(index, 1);
}
</script>

<template>
  <div class="block-container">
    <h3 class="block-header">계좌번호 블록</h3>
    <div class="account-list">
      <div v-for="(account, index) in data.accounts" :key="index" class="account-item">
        <button @click="removeAccount(index)" class="remove-account-button">
          X
        </button>
        <div class="input-group">
          <label class="input-label">은행</label>
          <input type="text" v-model="account.bank" class="text-input" placeholder="예: 국민은행">
        </div>
        <div class="input-group">
          <label class="input-label">계좌번호</label>
          <input type="text" v-model="account.number" class="text-input" placeholder="예: 123-456-7890">
        </div>
        <div class="input-group">
          <label class="input-label">예금주</label>
          <input type="text" v-model="account.name" class="text-input" placeholder="예: 홍길동">
        </div>
      </div>
    </div>
    <button @click="addAccount" class="add-account-button">
      + 계좌 추가
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

.account-list {
  display: flex;
  flex-direction: column;
  gap: 0.75rem; /* space-y-3 */
}

.account-item {
  padding: 0.75rem; /* p-3 */
  border: 1px solid #d1d5db; /* border border-gray-300 */
  border-radius: 0.5rem; /* rounded-lg */
  background-color: white; /* bg-white */
  display: flex;
  flex-direction: column;
  gap: 0.5rem; /* space-y-2 */
  position: relative;
}

.remove-account-button {
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
  opacity: 1; /* Always visible, Adjusted to match delete-button */
  transition: opacity 0.3s ease, transform 0.3s ease; /* Adjusted to match delete-button */
}

.account-item:hover .remove-account-button {
  transform: scale(1.1);
  background-color: #f5c6cb; /* Darker on hover */
  color: #721c24; /* Keep text color consistent */
}

.input-group {
  /* flex-direction: column; */
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
  padding: 0.25rem 0.5rem; /* p-1 */
  border: 1px solid #d1d5db; /* border border-gray-300 */
  border-radius: 0.375rem; /* rounded-md */
  outline: none; /* focus:outline-none */
  transition: all 0.2s ease;
}

.text-input:focus {
  border-color: #60a5fa; /* focus:ring-blue-400 */
  box-shadow: 0 0 0 2px rgba(96, 165, 250, 0.5); /* focus:ring-2 */
}

.add-account-button {
  width: 100%;
  font-size: 0.875rem; /* text-sm */
  background-color: #f3f4f6; /* bg-gray-100 */
  color: #4b5563; /* text-gray-700 */
  padding: 0.5rem 0.75rem; /* py-2 px-3 */
  border-radius: 0.375rem; /* rounded-md */
  margin-top: 0.75rem; /* mt-3 */
  border: 1px solid #d1d5db; /* border border-gray-300 */
  transition: background-color 0.2s ease;
}

.add-account-button:hover {
  background-color: #e5e7eb; /* hover:bg-gray-200 */
}
</style>