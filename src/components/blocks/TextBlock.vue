<script setup>
import { useEditor, EditorContent } from '@tiptap/vue-3';
import StarterKit from '@tiptap/starter-kit';

const props = defineProps({
  data: Object
});

const editor = useEditor({
  content: props.data.content,
  extensions: [
    StarterKit.configure({
      // Disable extensions we don't need for a simple text block
      heading: false,
      blockquote: false,
      codeBlock: false,
      horizontalRule: false,
      listItem: false,
      orderedList: false,
      bulletList: false,
    }),
  ],
  onUpdate: ({ editor }) => {
    // Sync the editor content back to the block data
    props.data.content = editor.getHTML();
  },
  editorProps: {
    attributes: {
      class: 'tiptap-editor-content', // Custom class for Tiptap content
    },
  },
});
</script>

<template>
  <div class="block-container">
    <h3 class="block-header">텍스트 블록</h3>
    <div v-if="editor" class="editor-wrapper">
      <div class="toolbar">
        <button @click="editor.chain().focus().toggleBold().run()" :class="{ 'is-active': editor.isActive('bold') }" class="toolbar-button">
          <b>B</b>
        </button>
        <button @click="editor.chain().focus().toggleItalic().run()" :class="{ 'is-active': editor.isActive('italic') }" class="toolbar-button">
          <i>I</i>
        </button>
      </div>
      <EditorContent :editor="editor" class="editor-content" />
    </div>
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

.editor-wrapper {
  background-color: white; /* bg-white */
  border-radius: 0.375rem; /* rounded-md */
  border: 1px solid #d1d5db; /* border border-gray-300 */
}

.toolbar {
  padding: 0.25rem; /* p-1 */
  border-bottom: 1px solid #e5e7eb; /* border-b border-gray-200 */
  display: flex;
  gap: 0.25rem; /* space-x-1 */
}

.toolbar-button {
  padding: 0.25rem 0.75rem; /* px-3 py-1 */
  background-color: transparent; /* bg-transparent */
  border: 0.1px solid rgb(191, 191, 191);
  font-size: 0.875rem; /* text-sm */
  transition: background-color 0.2s ease; /* transition-colors */
}

.toolbar-button:hover {
  background-color: #f3f4f6; /* hover:bg-gray-100 */
}

.toolbar-button.is-active {
  background-color: #DBEAFE; /* bg-blue-100 */
  color: #1D4ED8; /* text-blue-700 */
}

.tiptap-editor-content {
  padding: 0.5rem; /* p-2 */
  border-radius: 0.25rem; /* rounded */
  outline: none; /* focus:outline-none */
  min-height: 80px; /* min-h-[80px] */
}

/* Tiptap default styles for prose content */
.tiptap-editor-content :first-child {
  margin-top: 0;
}
.tiptap-editor-content :last-child {
  margin-bottom: 0;
}
</style>