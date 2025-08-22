<script setup>
import { computed } from 'vue';

const props = defineProps({
  isOpen: Boolean,
  blockType: String
});

const emit = defineEmits(['add-block']); // 'close' emit is removed

const blockTypeNames = {
  title: '제목',
  text: '텍스트',
  image: '이미지',
  gallery: '갤러리',
  dday: 'D-Day',
  contact: '연락처',
  account: '계좌번호',
};

const panelTitle = computed(() => {
  return `${blockTypeNames[props.blockType] || '블록'} 종류`;
});

// For now, just one default variation
const variations = computed(() => {
  if (props.blockType) {
    return [{ id: `${props.blockType}-default`, name: `${blockTypeNames[props.blockType]} 기본형`, type: props.blockType }];
  }
  return [];
});

function addSelectedBlock(variationType) {
  emit('add-block', variationType);
  // No longer emitting 'close' here, App.vue will handle closing via the toggle button
}
</script>

<template>
  <div class="variations-panel" :class="{ 'is-open': isOpen }">
    <!-- Removed panel-header and close button -->
    <div class="panel-content">
      <h3>{{ panelTitle }}</h3> <!-- Move title here -->
      <div 
        v-for="variation in variations" 
        :key="variation.id" 
        class="variation-item"
        @click="addSelectedBlock(variation.type)"
      >
        <div class="variation-thumbnail">
          <!-- Placeholder for thumbnail -->
          <p>{{ variation.name }}</p>
        </div>
        <p class="variation-name">{{ variation.name }}</p>
      </div>
    </div>
  </div>
</template>

<style scoped>
.variations-panel {
  width: 0; /* Default closed state */
  background-color: white;
  box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05);
  display: flex;
  flex-direction: column;
  border-right: 1px solid #e5e7eb;
  z-index: 50;
  height: 100vh;
  transition: width 0.3s ease-in-out; /* Transition for width */
  overflow: hidden; /* Hide content when closed */
}

.variations-panel.is-open {
  width: 18rem; /* Open state */
}

.panel-content {
  flex: 1;
  padding: 1rem;
  overflow-y: auto;
}

.panel-content h3 {
  margin-top: 0;
  margin-bottom: 1rem;
  font-size: 1.25rem;
  font-weight: 600;
}

.variation-item {
  border: 1px solid #eee;
  border-radius: 0.5rem;
  padding: 1rem;
  margin-bottom: 1rem;
  cursor: pointer;
  transition: all 0.2s;
}

.variation-item:hover {
  background-color: #f5f5f5;
  border-color: #ccc;
}

.variation-thumbnail {
  background-color: #e0e0e0;
  height: 100px;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-bottom: 0.5rem;
  border-radius: 0.25rem;
}

.variation-name {
  font-weight: 500;
  text-align: center;
}
</style>
