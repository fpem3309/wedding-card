<script setup>
// Reintroduce currentView prop
defineProps({
  currentView: String
});

const blockTypes = [
  { type: 'title', name: '제목', icon: '<svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16" /></svg>' }, // Text lines
  { type: 'text', name: '텍스트', icon: '<svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12h6m-6 4h6m2 5H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z" /></svg>' }, // Document with lines
  { type: 'image', name: '이미지', icon: '<svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 16l4.586-4.586a2 2 0 012.828 0L16 16m-2-2l1.586-1.586a2 2 0 012.828 0L20 14m-6-6h.01M6 20h12a2 2 0 002-2V6a2 2 0 00-2-2H6a2 2 0 00-2 2v12a2 2 0 002 2z" /></svg>' }, // Photo icon
  { type: 'gallery', name: '갤러리', icon: '<svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 8h14M5 8a2 2 0 110-4h14a2 2 0 110 4M5 8v10a2 2 0 002 2h10a2 2 0 002-2V8m-9 4h4" /></svg>' }, // Stack of photos
  { type: 'dday', name: 'D-Day', icon: '<svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 7V3m8 4V3m-9 8h10M5 21h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v12a2 2 0 002 2z" /></svg>' }, // Calendar icon
  { type: 'contact', name: '연락처', icon: '<svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 5a2 2 0 012-2h3.28a1 1 0 01.948.684l1.498 4.493a1 1 0 01-.502 1.21l-2.257 1.13a11.042 11.042 0 005.516 5.516l1.13-2.257a1 1 0 011.21-.502l4.493 1.498a1 1 0 01.684.949V19a2 2 0 01-2 2h-1C9.716 21 3 14.284 3 6V5z" /></svg>' }, // Phone icon
  { type: 'account', name: '계좌번호', icon: '<svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 9V7a2 2 0 00-2-2H5a2 2 0 00-2 2v6a2 2 0 002 2h2m2 4h10a2 2 0 002-2v-6a2 2 0 00-2-2H9a2 2 0 00-2 2v6a2 2 0 002 2zm7-5a2 2 0 11-4 0 2 2 0 014 0z" /></svg>' }, // Credit card icon
];

const emit = defineEmits(['open-block-variations']);

function selectView(type) {
  emit('open-block-variations', type);
}
</script>

<template>
  <div class="sidebar-menu">
    <ul>
      <li 
        v-for="block in blockTypes" 
        :key="block.type" 
        @click="selectView(block.type)"
        :class="{ 'active': currentView === block.type }" 
      >
        <div class="icon" v-html="block.icon"></div>
        <span class="text">{{ block.name }}</span>
      </li>
    </ul>
  </div>
</template>

<style scoped>
.sidebar-menu {
  width: 5rem; /* Narrower width */
  background-color: white; /* Changed to white */
  padding: 1rem 0.5rem; /* Adjusted padding */
  height: 100vh;
  border-right: 1px solid #e5e7eb; /* border-r border-gray-200 */
  display: flex; /* Use flex for vertical centering of ul */
  flex-direction: column;
  align-items: center;
}

ul {
  list-style: none;
  padding: 0;
  margin: 0;
  width: 100%; /* Take full width of sidebar-menu */
}

li {
  display: flex;
  flex-direction: column; /* Stack icon and text vertically */
  align-items: center; /* Center horizontally */
  padding: 0.75rem 0; /* Adjusted padding */
  cursor: pointer;
  border-radius: 0.5rem; /* rounded-lg */
  font-weight: 500; /* font-medium */
  color: #374151; /* text-gray-700 */
  transition: background-color 0.2s, color 0.2s;
  margin-bottom: 0.5rem; /* Space between items */
}

li:hover {
  background-color: #e5e7eb; /* hover:bg-gray-200 */
}

li.active {
  /* Removed background-color */
}

li.active .icon,
li.active .text {
  color: #ff69b4; /* Hot pink for active icon and text */
}

.icon {
  width: 1.5rem; /* Icon size */
  height: 1.5rem; /* Icon size */
  margin-bottom: 0.25rem; /* Space between icon and text */
  color: #4a5568; /* Icon color */
}

.text {
  font-size: 0.75rem; /* Smaller text */
  text-align: center;
  line-height: 1; /* Compact line height */
}
</style>
