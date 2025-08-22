<script setup>
import { ref, computed, watchEffect } from 'vue';

const props = defineProps({
  blocks: Array // D-Day needs to read from other blocks (specifically the title block)
});

const weddingDate = ref(null);
const dDayText = ref('');

// Function to parse date string and calculate D-Day
const calculateDday = () => {
  const titleBlock = props.blocks.find(block => block.type === 'title');
  if (titleBlock && titleBlock.data && titleBlock.data.date) {
    const dateString = titleBlock.data.date;
    // Attempt to parse various date formats (e.g., "2025년 10월 25일 토요일 오후 2시")
    // This is a simplified parser. For robust parsing, a library like 'date-fns' would be better.
    const yearMatch = dateString.match(/(\d{4})년/);
    const monthMatch = dateString.match(/(\d{1,2})월/);
    const dayMatch = dateString.match(/(\d{1,2})일/);

    if (yearMatch && monthMatch && dayMatch) {
      const year = parseInt(yearMatch[1]);
      const month = parseInt(monthMatch[1]) - 1; // Month is 0-indexed
      const day = parseInt(dayMatch[1]);
      
      const targetDate = new Date(year, month, day);
      targetDate.setHours(0, 0, 0, 0); // Set to start of day for accurate D-Day

      const today = new Date();
      today.setHours(0, 0, 0, 0); // Set to start of day

      const diffTime = targetDate.getTime() - today.getTime();
      const diffDays = Math.ceil(diffTime / (1000 * 60 * 60 * 24));

      if (diffDays > 0) {
        dDayText.value = `D-${diffDays}`;
      } else if (diffDays === 0) {
        dDayText.value = `D-Day`;
      } else {
        dDayText.value = `D+${Math.abs(diffDays)}`;
      }
    } else {
      dDayText.value = '날짜 형식을 확인해주세요.';
    }
  } else {
    dDayText.value = '예식 날짜를 입력해주세요.';
  }
};

// Watch for changes in blocks data to recalculate D-Day
watchEffect(() => {
  calculateDday();
});
</script>

<template>
  <div class="preview-dday-container">
    <h2 class="dday-text">
      <span class="dday-value">{{ dDayText }}</span>
    </h2>
    <p class="dday-date">
      <span v-if="weddingDate">
        {{ weddingDate.toLocaleDateString('ko-KR', { year: 'numeric', month: 'long', day: 'numeric' }) }}
      </span>
    </p>
  </div>
</template>

<style scoped>
.preview-dday-container {
  padding: 1.5rem 1rem; /* py-6 px-4 */
  text-align: center;
  background-color: white; /* bg-white */
}

.dday-text {
  font-size: 1.875rem; /* text-3xl */
  font-weight: 700; /* font-bold */
  color: #1f2937; /* text-gray-800 */
  margin-bottom: 0.5rem; /* mb-2 */
}

.dday-value {
  color: #ef4444; /* text-red-500 */
}

.dday-date {
  font-size: 1.125rem; /* text-lg */
  color: #4b5563; /* text-gray-600 */
  font-weight: 500; /* font-medium */
}
</style>