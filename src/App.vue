<script setup>
import { ref } from 'vue';
import Editor from './components/common/Editor.vue';
import Preview from './components/common/Preview.vue';
import BlockSelector from './components/common/BlockSelector.vue';

// The single source of truth for the invitation content.
const blocks = ref([
  {
    id: 'block-1',
    type: 'title',
    data: {
      groomName: '신랑이름',
      brideName: '신부이름',
      date: '2025년 10월 25일 토요일 오후 2시',
      location: '더채플앳웨스트'
    }
  },
  {
    id: 'block-2',
    type: 'text',
    data: {
      content: '서로를 보듬어주고 아껴주며, 예쁘게 살겠습니다.'
    }
  }
]);

const showBlockSelector = ref(false); // State for BlockSelector visibility

function addBlock(type) {
  const newBlock = {
    id: `block-${Date.now()}`,
    type: type,
    data: {}
  };

  if (type === 'text') {
    newBlock.data.content = '새로운 텍스트 블록입니다.';
  } else if (type === 'gallery') {
    newBlock.data.images = [
    ];
  } else if (type === 'image') {
    newBlock.data.src = "data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='800' height='600' viewBox='0 0 800 600'%3E%3Crect width='800' height='600' fill='%23e0e0e0'/%3E%3Ctext x='50%25' y='50%25' font-family='Arial' font-size='40' fill='%23888' text-anchor='middle' dominant-baseline='middle'%3EUpload Image%3C/text%3E%3C/svg%3E";
    newBlock.data.caption = '하나뿐인 소중한 순간';
  } else if (type === 'account') {
    newBlock.data.accounts = [
      { bank: '국민은행', number: '123-456-7890', name: '홍길동' }
    ];
  } else if (type === 'dday') {
    // D-Day block doesn't need specific data, it derives it from other blocks
  }

  blocks.value.push(newBlock);
  // showBlockSelector.value = false; // Do not close selector after adding
}

function deleteBlock(id) {
  const index = blocks.value.findIndex(b => b.id === id);
  if (index !== -1) {
    blocks.value.splice(index, 1);
  }
}

function toggleBlockSelector() {
  showBlockSelector.value = !showBlockSelector.value;
}
</script>

<template>
  <div class="app-container">
    <!-- Left: Editor Panel -->
    <div :class="['editor-panel', { 'sidebar-open-offset': showBlockSelector }]">
      <Editor :blocks="blocks" @add-block="addBlock" @delete-block="deleteBlock" @open-block-selector="toggleBlockSelector" />
    </div>

    <!-- Right: Preview Area -->
    <div class="preview-area">
      <Preview :blocks="blocks" />
    </div>

    <!-- Block Selector Sidebar -->
    <Transition name="sidebar-transition">
      <BlockSelector v-if="showBlockSelector" :is-open="showBlockSelector" @select-block-type="addBlock" @close="showBlockSelector = false" />
    </Transition>

    <!-- Toggle Button for Block Selector -->
    <button @click="toggleBlockSelector" :class="['toggle-sidebar-button', { 'is-open': showBlockSelector }]">
      <span v-if="showBlockSelector">&lt;</span>
      <span v-else>&gt;</span>
    </button>
  </div>
</template>

<style scoped>
.app-container {
  display: flex;
  height: 100vh;
  background: linear-gradient(to bottom right, #e0f2fe, #ede9fe); /* from-blue-50 to-purple-50 */
  font-family: sans-serif; /* font-sans */
  color: #2d3748; /* text-gray-800 */
}

.editor-panel {
  width: 24rem; /* w-96 */
  background-color: white; /* bg-white */
  /* overflow-y: auto; */ /* Removed to let inner container handle scroll */
  box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.1), 0 10px 10px -5px rgba(0, 0, 0, 0.04); /* shadow-xl */
  display: flex;
  flex-direction: column;
  border-top-right-radius: 1rem; /* rounded-r-2xl */
  border-bottom-right-radius: 1rem;
  transition: transform 0.3s ease-out; /* Add transition */
}

.editor-panel.sidebar-open-offset {
  transform: translateX(16rem); /* Push right by sidebar width */
}

.preview-area {
  flex: 1;
  display: flex;
  /* align-items: center; */ /* Removed to allow scroll to top */
  /* justify-content: center; */ /* Removed to allow scroll to top */
  /* padding: 2rem; */ /* Moved to inner element in Preview.vue */
  overflow-y: auto; /* Allow preview area to scroll */
}

/* Transition for BlockSelector */
.sidebar-transition-enter-active,
.sidebar-transition-leave-active {
  transition: opacity 0.3s ease-out, transform 0.3s ease-out;
}

.sidebar-transition-enter-from,
.sidebar-transition-leave-to {
  opacity: 0;
  transform: translateX(-100%);
}

.toggle-sidebar-button {
  position: fixed;
  top: 50%;
  transform: translateY(-50%) translateX(0); /* Initial transform for vertical centering */
  --translate-x-value: 0; /* Define CSS variable for translateX */
  width: 3rem;
  height: 3.5rem;
  background-color: #2563eb;
  color: white;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 1.5rem;
  box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -2px rgba(0, 0, 0, 0.06);
  transition: transform 0.3s ease-out; /* Changed to transform transition */
  z-index: 51;
  clip-path: polygon(0 0, 100% 15%, 100% 85%, 0% 100%);
  border-top-right-radius: 0.5rem;
  border-bottom-right-radius: 0.5rem;
}

.toggle-sidebar-button.is-open {
  transform: translateY(-50%) translateX(16rem); /* Move with sidebar */
  --translate-x-value: 16rem; /* Update variable for open state */
}

.toggle-sidebar-button:hover {
  background-color: #1d4ed8;
  transform: translateY(-50%) translateX(var(--translate-x-value)) scale(1.05); /* Use variable for translateX */
}
</style>