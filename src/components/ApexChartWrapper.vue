<template>
  <div ref="chart"></div>
</template>

<script setup lang="ts">
import { ref, onMounted, watch, onBeforeUnmount } from 'vue';
import ApexCharts, { type ApexOptions } from 'apexcharts';

const chart = ref<HTMLElement | null>(null);
let apexChart: ApexCharts | null = null;

const props = defineProps<{
  options: ApexOptions;
}>();

onMounted(() => {
  if (chart.value) {
    apexChart = new ApexCharts(chart.value, props.options);
    apexChart.render();
  }
});

watch(() => props.options, (newOptions) => {
  if (apexChart) {
    apexChart.updateOptions(newOptions);
  }
}, { deep: true });

onBeforeUnmount(() => {
  if (apexChart) {
    apexChart.destroy();
  }
});
</script>
