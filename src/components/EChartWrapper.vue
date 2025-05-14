<template>
  <div ref="chart" :style="{ width, height }"></div>
</template>

<script setup lang="ts">
import { ref, onMounted, onBeforeUnmount, watch, defineProps, withDefaults } from 'vue';
import * as echarts from 'echarts';
import type { EChartsOption } from 'echarts';

const chart = ref<HTMLElement | null>(null);
let echartInstance: echarts.ECharts | null = null;

const props = withDefaults(defineProps<{
  options: EChartsOption | null;  
  width?: string;
  height?: string;
}>(), {
  width: '100%',
  height: '400px',
  options: null
});

onMounted(() => {
  if (chart.value) {
    echartInstance = echarts.init(chart.value);
    if (props.options) {
      echartInstance.setOption(props.options);
    }

    const resizeObserver = new ResizeObserver(() => {
      echartInstance?.resize();
    });
    resizeObserver.observe(chart.value);

    onBeforeUnmount(() => {
      resizeObserver.disconnect();
    });
  }
});

watch(() => props.options, (newOptions) => {
  if (echartInstance && newOptions) {
    echartInstance.setOption(newOptions);
  }
}, { deep: true });

onBeforeUnmount(() => {
  if (echartInstance) {
    echartInstance.dispose();
  }
});
</script>
