<script setup>
const props = defineProps({
  data: Object
});

// Initialize contacts array if it doesn't exist
if (!props.data.contacts) {
  props.data.contacts = [];
}

function addContact() {
  props.data.contacts.push({ role: '', name: '', phone: '' });
}

function removeContact(index) {
  props.data.contacts.splice(index, 1);
}
</script>

<template>
  <div class="block-container">
    <h3 class="block-header">연락처 블록</h3>
    <div class="contact-list">
      <div v-for="(contact, index) in data.contacts" :key="index" class="contact-item">
        <button @click="removeContact(index)" class="remove-contact-button">
          X
        </button>
        <div class="input-group">
          <label class="input-label">역할</label>
          <input type="text" v-model="contact.role" class="text-input" placeholder="예: 신랑, 신부, 신랑측 혼주">
        </div>
        <div class="input-group">
          <label class="input-label">이름</label>
          <input type="text" v-model="contact.name" class="text-input" placeholder="예: 홍길동">
        </div>
        <div class="input-group">
          <label class="input-label">연락처</label>
          <input type="text" v-model="contact.phone" class="text-input" placeholder="예: 010-1234-5678">
        </div>
      </div>
    </div>
    <button @click="addContact" class="add-contact-button">
      + 연락처 추가
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

.contact-list {
  display: flex;
  flex-direction: column;
  gap: 0.75rem; /* space-y-3 */
}

.contact-item {
  padding: 0.75rem; /* p-3 */
  border: 1px solid #d1d5db; /* border border-gray-300 */
  border-radius: 0.5rem; /* rounded-lg */
  background-color: white; /* bg-white */
  display: flex;
  flex-direction: column;
  gap: 0.5rem; /* space-y-2 */
  position: relative;
}

.remove-contact-button {
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

.contact-item:hover .remove-contact-button {
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

.add-contact-button {
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

.add-contact-button:hover {
  background-color: #e5e7eb; /* hover:bg-gray-200 */
}
</style>