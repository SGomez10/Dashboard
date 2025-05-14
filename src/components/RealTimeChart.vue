<template>
  <div class="real-time-chart">
    <div class="chart-title">{{ title }}</div>
    <ChartJsWrapper
      ref="chart"
      type="line"
      :data="chartData"
      :options="chartOptions"
    />
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted, onBeforeUnmount, computed } from 'vue';
import ChartJsWrapper from './ChartJsWrapper.vue';
import type { ChartData, ChartOptions } from 'chart.js';

const props = defineProps<{
  title: string;
  initialData: number[];
  labels: string[];
  maxPoints?: number;
}>();

const chartData = ref<ChartData<'line'>>({
  labels: props.labels,
  datasets: [{
    label: props.title,
    data: props.initialData,
    borderColor: '#4CAF50',
    backgroundColor: 'rgba(76, 175, 80, 0.1)',
    tension: 0.4,
    fill: true
  }]
});

const chartOptions = ref<ChartOptions<'line'>>({
  responsive: true,
  maintainAspectRatio: false,
  animation: {
    duration: 0
  },
  scales: {
    y: {
      beginAtZero: false
    }
  }
});

let intervalId: number | null = null;
const maxDataPoints = props.maxPoints || 20;

const addDataPoint = (value: number) => {
  const newData = [...chartData.value.datasets[0].data];
  const newLabels = [...chartData.value.labels as string[]];
  
  if (newData.length >= maxDataPoints) {
    newData.shift();
    newLabels.shift();
  }
  
  newData.push(value);
  newLabels.push(new Date().toLocaleTimeString());
  
  chartData.value = {
    labels: newLabels,
    datasets: [{
      ...chartData.value.datasets[0],
      data: newData
    }]
  };
};

onMounted(() => {
  intervalId = window.setInterval(() => {
    const lastValue = chartData.value.datasets[0].data.length > 0 
      ? chartData.value.datasets[0].data[chartData.value.datasets[0].data.length - 1] as number
      : 0;
    const fluctuation = (Math.random() - 0.5) * 20;
    const newValue = Math.max(0, lastValue + fluctuation);
    addDataPoint(newValue);
  }, 2000);
});

onBeforeUnmount(() => {
  if (intervalId) {
    clearInterval(intervalId);
  }
});
</script>

<style scoped>
.real-time-chart {
  background: #1E1E1E;
  border-radius: 8px;
  padding: 1rem;
  color: white;
  height: 100%;
}
.chart-title {
  font-weight: bold;
  margin-bottom: 10px;
  text-align: center;
}
</style>