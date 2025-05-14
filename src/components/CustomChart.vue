<template>
  <div class="custom-chart">
    <div class="chart-title">{{ title }}</div>
    <div class="chart-container">
      <svg :width="width" :height="height">
        <rect 
          v-for="(item, index) in data" 
          :key="index"
          :x="index * (width / data.length)" 
          :y="height - (item.value * height / maxValue)"
          :width="(width / data.length) - 2" 
          :height="item.value * height / maxValue"
          :fill="item.color"
          rx="2"
        />
        <text 
          v-for="(item, index) in data" 
          :key="'label-'+index"
          :x="index * (width / data.length) + (width / data.length / 2)" 
          :y="height - 5"
          text-anchor="middle"
          fill="#fff"
          font-size="10"
        >
          {{ item.label }}
        </text>
      </svg>
    </div>
  </div>
</template>

<script setup lang="ts">
import { computed } from 'vue';

interface ChartItem {
  label: string;
  value: number;
  color: string;
}

const props = withDefaults(defineProps<{
  title: string;
  data: ChartItem[];
  width?: number;
  height?: number;
}>(), {
  width: 300,
  height: 200,
});

const maxValue = computed(() => Math.max(...props.data.map(item => item.value)));
</script>

<style scoped>
.custom-chart {
  background: #1E1E1E;
  border-radius: 8px;
  padding: 1rem;
  color: white;
}
.chart-title {
  font-weight: bold;
  margin-bottom: 10px;
  text-align: center;
}
.chart-container {
  display: flex;
  justify-content: center;
}
</style>