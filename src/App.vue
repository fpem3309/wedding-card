<script setup>
import { ref, computed } from 'vue';
import Editor from './components/common/Editor.vue';
import Preview from './components/common/Preview.vue';
import SidebarMenu from './components/common/SidebarMenu.vue';
import BlockVariationsPanel from './components/common/BlockVariationsPanel.vue';

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

// State for BlockVariationsPanel
const showVariationsPanel = ref(false);
const selectedBlockTypeForVariations = ref(null); // This will now retain its value

function openVariations(type) {
  selectedBlockTypeForVariations.value = type; 
  showVariationsPanel.value = true;
}

function toggleVariationsPanel() {
  showVariationsPanel.value = !showVariationsPanel.value;
  if (showVariationsPanel.value && selectedBlockTypeForVariations.value === null) {
    // If opening and no type was previously selected (initial load/refresh), default to 'title'
    selectedBlockTypeForVariations.value = 'title';
  }
  // IMPORTANT: Do NOT set selectedBlockTypeForVariations to null when closing
}

function addBlock(type) {
  const newBlock = {
    id: `block-${Date.now()}`,
    type: type,
    data: {}
  };

  if (type === 'text') {
    newBlock.data.content = '새로운 텍스트 블록입니다.';
  } else if (type === 'gallery') {
    newBlock.data.images = [];
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
}

function deleteBlock(id) {
  const index = blocks.value.findIndex(b => b.id === id);
  if (index !== -1) {
    blocks.value.splice(index, 1);
  }
}

function updateBlocks(newBlocks) {
  blocks.value = newBlocks;
}
</script>

<template>
  <div class="app-container">
    <!-- Sidebar Menu (Leftmost) -->
    <SidebarMenu 
      @open-block-variations="openVariations" 
      :current-view="selectedBlockTypeForVariations" 
    />

    <!-- Block Variations Panel (Next to Sidebar, always in DOM, width controlled by class) -->
    <BlockVariationsPanel 
      :is-open="showVariationsPanel" 
      :block-type="selectedBlockTypeForVariations"
      @add-block="addBlock"
    />

    <!-- Toggle Button for Block Variations Panel -->
    <button 
      @click="toggleVariationsPanel" 
      :class="['toggle-variations-panel-button', { 'is-open': showVariationsPanel }]">
      <span v-if="showVariationsPanel">&lt;</span>
      <span v-else>&gt;</span>
    </button>

    <!-- Main Content Area (Editor + Preview) -->
    <div class="main-content-area">
      <!-- Editor Panel -->
      <div class="editor-panel">
        <Editor 
          :blocks="blocks" 
          @add-block="addBlock" 
          @delete-block="deleteBlock"
          @update:blocks="updateBlocks"
        />
      </div>

      <!-- Preview Area -->
      <div class="preview-area">
        <Preview :blocks="blocks" />
      </div>
    </div>
  </div>
</template>

<style scoped>
.app-container {
  display: flex;
  height: 100vh;
  background: linear-gradient(to bottom right, #f0f4f8, #e6e9f0);
  font-family: 'Pretendard', sans-serif;
  color: #333;
  position: relative; /* For positioning the toggle button */
}

.main-content-area {
  display: flex;
  flex: 1; /* Takes remaining space */
}

.editor-panel {
  width: 28rem; /* Fixed width for editor */
  background-color: white;
  box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05);
  display: flex;
  flex-direction: column;
  border-right: 1px solid #e5e7eb;
  z-index: 10;
}

.preview-area {
  flex: 1; /* Takes remaining space in main-content-area */
  display: flex;
  justify-content: center;
  overflow-y: auto;
  padding: 2rem;
}

.toggle-variations-panel-button {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  left: calc(5rem + 0px); /* SidebarMenu new width + 0px (when closed) */
  width: 2rem;
  height: 3.5rem;
  background-color: #2563eb;
  color: white;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 1.5rem;
  box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -2px rgba(0, 0, 0, 0.06);
  transition: left 0.3s ease-in-out; /* Transition for position */
  z-index: 51; /* Above panels */
  border-top-right-radius: 0.5rem;
  border-bottom-right-radius: 0.5rem;
  border: none;
  cursor: pointer;
}

.toggle-variations-panel-button.is-open {
  left: calc(5rem + 18rem); /* SidebarMenu width + BlockVariationsPanel width */
  border-top-left-radius: 0.5rem; /* Change border radius when open */
  border-bottom-left-radius: 0.5rem;
  border-top-right-radius: 0;
  border-bottom-right-radius: 0;
}

.toggle-variations-panel-button:hover {
  background-color: #1d4ed8;
}
</style>
