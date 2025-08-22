<script setup>
import { ref } from 'vue';
import draggable from 'vuedraggable';
import TitleBlock from '../blocks/TitleBlock.vue';
import TextBlock from '../blocks/TextBlock.vue';
import GalleryBlock from '../blocks/GalleryBlock.vue';
import ImageBlock from '../blocks/ImageBlock.vue';
import AccountBlock from '../blocks/AccountBlock.vue';
import DdayBlock from '../blocks/DdayBlock.vue';
import ContactBlock from '../blocks/ContactBlock.vue';
// BlockSelector is no longer imported here, as it's rendered in App.vue

defineProps({
  blocks: Array
});

const emit = defineEmits(['addBlock', 'deleteBlock', 'openBlockSelector']); // Keep openBlockSelector emit

const componentMap = {
  title: TitleBlock,
  text: TextBlock,
  gallery: GalleryBlock,
  image: ImageBlock,
  account: AccountBlock,
  dday: DdayBlock,
  contact: ContactBlock,
};

function addBlock(type) {
  emit('addBlock', type);
}

function deleteBlock(id) {
  emit('deleteBlock', id);
}

function openBlockSelector() { // This function is still needed to emit the event
  emit('openBlockSelector');
}
</script>

<template>
  <div class="editor-container">
    <div class="block-list-container">
      <draggable
        :list="blocks"
        item-key="id"
        class="block-list"
        handle=".handle"
      >
        <template #item="{ element: block }">
          <div class="block-item-wrapper">
            <div class="handle">
              <svg xmlns="http://www.w3.org/2000/svg" class="handle-icon" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16m-7 6h7" />
              </svg>
            </div>
            <button @click="deleteBlock(block.id)" class="delete-button">
              <svg xmlns="http://www.w3.org/2000/svg" class="delete-icon" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
              </svg>
            </button>
            <component :is="componentMap[block.type]" :data="block.data" />
          </div>
        </template>
      </draggable>
    </div>

    <!-- The "Add Block" button is now outside this component, in App.vue -->
    <!-- The BlockSelector is also rendered in App.vue -->
  </div>
</template>

<style scoped>
.editor-container {
  padding: 3rem; /* Increased padding for editor space */
  background-color: white; /* bg-white */
  height: 100%; /* h-full */
  display: flex;
  flex-direction: column;
}

.editor-header {
  font-size: 1.875rem; /* text-3xl */
  font-weight: 800; /* font-extrabold */
  color: #1e40af; /* text-blue-800 */
  margin-bottom: 2rem; /* mb-8 */
  text-align: center;
}

.block-list-container {
  flex: 1; /* flex-1 */
  overflow-y: auto;
  padding-right: 0.5rem; /* pr-2 */
  margin-right: -0.5rem; /* -mr-2 */
  position: relative;
}

.block-list {
  display: flex;
  flex-direction: column;
  gap: 1.5rem; /* space-y-6 */
}

.block-item-wrapper {
  position: relative;
  padding-top: 0.5rem; /* pt-2 */
  min-height: 5rem; /* Ensure minimum height */
  overflow: visible; /* Ensure content is not clipped */
}

.handle {
  position: absolute;
  left: -2.5rem; /* More space from block */
  top: 50%;
  transform: translateY(-50%);
  cursor: grab;
  opacity: 0;
  transition: opacity 0.3s ease;
  padding: 0.5rem; /* p-2 */
  border-radius: 9999px; /* rounded-full */
  background-color: #f3f4f6; /* bg-gray-100 */
}

.block-item-wrapper:hover .handle {
  opacity: 1;
  background-color: #e5e7eb; /* hover:bg-gray-200 */
}

.handle-icon {
  height: 1.25rem; /* h-5 */
  width: 1.25rem; /* w-5 */
  color: #6b7280; /* text-gray-500 */
}

.delete-button {
  position: absolute;
  top: 0.5rem; /* Adjusted for padding */
  right: 0.5rem; /* Adjusted for padding */
  z-index: 10;
  padding: 0.25rem; /* p-1 */
  background-color: #f8d7da; /* Very light red/pink */
  color: #721c24; /* Darker red for text */
  border: 1px solid #f5c6cb; /* Subtle border */
  border-radius: 9999px; /* rounded-full */
  width: 1.75rem; /* w-7 */
  height: 1.75rem; /* h-7 */
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 0.875rem; /* text-sm */
  opacity: 1;
  transition: opacity 0.3s ease, transform 0.3s ease;
}

.block-item-wrapper:hover .delete-button {
  transform: scale(1.1); /* group-hover:scale-110 */
}

.delete-icon {
  height: 1rem; /* h-4 */
  width: 1rem; /* w-4 */
}

/* Removed add-block-section and add-block-button styles */
</style>