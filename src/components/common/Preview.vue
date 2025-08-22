<script setup>
import TitlePreview from '../previews/TitlePreview.vue';
import TextPreview from '../previews/TextPreview.vue';
import GalleryPreview from '../previews/GalleryPreview.vue';
import ImagePreview from '../previews/ImagePreview.vue';
import AccountPreview from '../previews/AccountPreview.vue';
import DdayPreview from '../previews/DdayPreview.vue';
import ContactPreview from '../previews/ContactPreview.vue';

defineProps({
  blocks: Array
});

const componentMap = {
  title: TitlePreview,
  text: TextPreview,
  gallery: GalleryPreview,
  image: ImagePreview,
  account: AccountPreview,
  dday: DdayPreview,
  contact: ContactPreview,
};
</script>

<template>
  <!-- This is now the root element, styled as the mobile preview canvas -->
  <div class="w-full max-w-sm bg-white rounded-2xl shadow-2xl overflow-hidden ring-4 ring-gray-300">
    <div class="overflow-y-auto">
      <div style="padding: 2rem;"> <!-- New div for padding -->
        <div v-for="block in blocks" :key="block.id">
          <component :is="componentMap[block.type]" :data="block.data" :blocks="blocks" />
        </div>
      </div>
    </div>
  </div>
</template>