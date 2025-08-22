<script setup>
defineProps({
  data: Object
});

function formatPhoneNumber(phoneNumber) {
  // Basic formatting for display, e.g., 01012345678 -> 010-1234-5678
  const cleaned = ('' + phoneNumber).replace(/\D/g, '');
  const match = cleaned.match(/^(\d{3})(\d{4})(\d{4})$/);
  if (match) {
    return `${match[1]}-${match[2]}-${match[3]}`;
  }
  return phoneNumber; // Return original if not a standard 11-digit number
}
</script>

<template>
  <div class="preview-contact-container">
    <h2 class="preview-contact-header">연락처</h2>
    <div v-if="data.contacts && data.contacts.length" class="contact-list">
      <div v-for="(contact, index) in data.contacts" :key="index" class="contact-item">
        <div class="contact-details">
          <p class="contact-role">{{ contact.role }}</p>
          <p class="contact-name">{{ contact.name }}</p>
          <p class="contact-phone">{{ formatPhoneNumber(contact.phone) }}</p>
        </div>
        <a :href="`tel:${contact.phone}`" class="call-button">
          전화걸기
        </a>
      </div>
    </div>
  </div>
</template>

<style scoped>
.preview-contact-container {
  padding: 1.5rem 1rem; /* py-6 px-4 */
  text-align: center;
  background-color: white; /* bg-white */
}

.preview-contact-header {
  font-size: 1.25rem; /* text-xl */
  font-family: serif; /* font-serif */
  margin-bottom: 1rem; /* mb-4 */
  color: #1f2937; /* text-gray-800 */
}

.contact-list {
  display: flex;
  flex-direction: column;
  gap: 0.75rem; /* space-y-3 */
  max-width: 12rem; /* max-w-xs */
  margin-left: auto; /* mx-auto */
  margin-right: auto; /* mx-auto */
}

.contact-item {
  padding: 0.75rem; /* p-3 */
  background-color: #f3f4f6; /* bg-gray-100 */
  border-radius: 0.5rem; /* rounded-lg */
  text-align: left;
  border: 1px solid #e5e7eb; /* border border-gray-200 */
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.contact-details {
  /* flex-direction: column; */
}

.contact-role {
  font-weight: 600; /* font-semibold */
  color: #4b5563; /* text-gray-700 */
}

.contact-name {
  font-size: 0.875rem; /* text-sm */
  color: #4b5563; /* text-gray-600 */
}

.contact-phone {
  font-size: 0.875rem; /* text-sm */
  color: #6b7280; /* text-gray-500 */
}

.call-button {
  font-size: 0.875rem; /* text-sm */
  padding: 0.25rem 0.75rem; /* px-3 py-1 */
  border-radius: 9999px; /* rounded-full */
  background-color: #3b82f6; /* bg-blue-500 */
  color: white;
  transition: all 0.2s ease; /* transition */
  box-shadow: 0 1px 2px 0 rgba(0, 0, 0, 0.05); /* shadow-sm */
}

.call-button:hover {
  background-color: #2563eb; /* hover:bg-blue-600 */
}
</style>