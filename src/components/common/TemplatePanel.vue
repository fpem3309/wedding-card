<script setup>
import { computed } from 'vue';

const props = defineProps({
  isOpen: Boolean,
  templates: Object // Pass templates object
});

const emit = defineEmits(['apply-template']);

function selectTemplate(templateId) {
  emit('apply-template', templateId);
}
</script>

<template>
  <div class="template-panel" :class="{ 'is-open': isOpen }">
    <div class="panel-content">
      <h3>템플릿 선택</h3>
      <div 
        v-for="(template, id) in templates" 
        :key="id" 
        class="template-item"
        @click="selectTemplate(id)"
      >
        <div class="template-thumbnail">
          <!-- Placeholder for template thumbnail -->
          <p>{{ template.name }}</p>
        </div>
        <p class="template-name">{{ template.name }}</p>
      </div>
    </div>
  </div>
</template>

<style scoped>
.template-panel {
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

.template-panel.is-open {
  width: 18rem; /* Open state - same width as BlockVariationsPanel */
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

.template-item {
  border: 1px solid #eee;
  border-radius: 0.5rem;
  padding: 1rem;
  margin-bottom: 1rem;
  cursor: pointer;
  transition: all 0.2s;
}

.template-item:hover {
  background-color: #f5f5f5;
  border-color: #ccc;
}

.template-thumbnail {
  background-color: #e0e0e0;
  height: 100px;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-bottom: 0.5rem;
  border-radius: 0.25rem;
}

.template-name {
  font-weight: 500;
  text-align: center;
}
</style>
