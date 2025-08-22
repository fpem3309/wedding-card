<script setup>
const props = defineProps({ isOpen: Boolean });
const emit = defineEmits(['selectBlockType', 'close']);

const blockTypes = [
  { type: 'text', label: '텍스트 블록', icon: '📝' },
  { type: 'image', label: '이미지 블록', icon: '🖼️' },
  { type: 'gallery', label: '갤러리 블록', icon: '🏞️' },
  { type: 'account', label: '계좌번호 블록', icon: '🏦' },
  { type: 'dday', label: 'D-Day 블록', icon: '🗓️' },
  { type: 'contact', label: '연락처 블록', icon: '📞' },
];

function selectType(type) {
  emit('selectBlockType', type);
}

function closePanel() {
  emit('close');
}
</script>

<template>
  <div class="sidebar-overlay">
    <div :class="['sidebar-panel', { 'is-open': props.isOpen }]">
      <h3 class="sidebar-header">블록 추가</h3>
      <div class="block-type-list">
        <button
          v-for="blockType in blockTypes"
          :key="blockType.type"
          @click="selectType(blockType.type)"
          class="block-type-button"
        >
          <span class="block-type-icon">{{ blockType.icon }}</span>
          <span>{{ blockType.label }}</span>
        </button>
      </div>
      <button @click="closePanel" class="close-button">
        닫기
      </button>
    </div>
  </div>
</template>

<style scoped>



.sidebar-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background-color: transparent; /* Removed darkening effect */
  pointer-events: none; /* Allow clicks through overlay */
  z-index: 50; /* Below the toggle button (z-index: 51) */
}

.sidebar-panel {
  position: absolute;
  top: 0;
  left: 0;
  height: 100%;
  width: 16rem; /* Changed from 20rem to 16rem */
  background-color: white;
  box-shadow: 0 0 15px rgba(0, 0, 0, 0.2); /* Stronger shadow */
  display: flex;
  flex-direction: column;
  padding: 2rem; /* p-8 */
  pointer-events: auto; /* Allow clicks on the sidebar panel */
}


.sidebar-panel.is-open {
  /* No transform here, handled by App.vue's Transition */
}

.sidebar-header {
  font-size: 1.5rem; /* text-2xl */
  font-weight: 700; /* font-bold */
  color: #1f2937; /* text-gray-800 */
  margin-bottom: 1.5rem; /* mb-6 */
  text-align: center;
}

.block-type-list {
  display: flex;
  flex-direction: column;
  gap: 0.75rem; /* space-y-3 */
  flex-grow: 1; /* Allow list to grow and push close button down */
}

.block-type-button {
  width: 100%;
  display: flex;
  align-items: center;
  padding: 1rem;
  border-radius: 0.75rem; /* Slightly more rounded */
  background-color: #f0f4f8; /* Lighter background */
  color: #2c3e50; /* Darker text for contrast */
  font-weight: 600;
  transition: all 0.2s ease;
  /* box-shadow: none; */ /* Removed box-shadow */
  pointer-events: auto; /* Re-enable clicks on the button */
}

.block-type-button:hover {
  background-color: #e0e7ed; /* Slightly darker on hover */
  transform: translateY(-0.125rem); /* Keep subtle lift */
}

.block-type-icon {
  font-size: 1.5rem; /* text-2xl */
  margin-right: 1rem; /* mr-4 */
}

.close-button {
  margin-top: 2rem; /* mt-8 */
  width: 100%;
  color: #2c3e50; /* Darker text for contrast */
  font-weight: 600; /* font-semibold */
  padding: 0.75rem 1rem; /* py-3 px-4 */
  border-radius: 0.75rem; /* Consistent with block-type-button */
  transition: all 0.2s ease; /* transition-colors */
  pointer-events: auto; /* Re-enable clicks on the button */
}

.toggle-sidebar-button {
  position: fixed;
  top: 50%;
  transform: translateY(-50%); /* Initial transform for vertical centering */
  width: 3rem;
  height: 3.5rem;
  background-color: red; /* DEBUG */
  border: 5px solid yellow; /* DEBUG */
  /* clip-path: polygon(0 0, 100% 15%, 100% 85%, 0% 100%); */
}

.toggle-sidebar-button.is-open {
  left: 16rem; /* Position next to the open sidebar */
}

.toggle-sidebar-button:hover {
  background-color: #1d4ed8;
  transform: translateY(-50%) scale(1.05); /* Only scale on hover, left is handled by is-open */
}
</style>