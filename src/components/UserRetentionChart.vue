<template>
  <div ref="chartRef" class="chart-container"></div>
</template>

<script setup lang="ts">
import * as echarts from 'echarts/core'
import {
  LineChart
} from 'echarts/charts'
import {
  TitleComponent,
  TooltipComponent,
  GridComponent,
  LegendComponent,
  DatasetComponent
} from 'echarts/components'
import { CanvasRenderer } from 'echarts/renderers'
import { onMounted, onBeforeUnmount, ref, nextTick } from 'vue'

echarts.use([
  TitleComponent,
  TooltipComponent,
  GridComponent,
  LegendComponent,
  DatasetComponent,
  LineChart,
  CanvasRenderer
])

const chartRef = ref<HTMLDivElement | null>(null)
let chartInstance: echarts.ECharts | null = null

const option = {
  backgroundColor: '#1E1E1E',
  title: {
    text: 'Evolución de Retención de Usuarios Nuevos',
    left: 'center',
    textStyle: { color: 'white' }
  },
  tooltip: { trigger: 'axis' },
  legend: {
    data: ['Retención de Usuarios (%)'],
    textStyle: { color: 'white' },
    top: 30
  },
  grid: {
    left: '5%',
    right: '5%',
    bottom: '10%',
    containLabel: true
  },
  xAxis: {
    type: 'category',
    data: ['Enero', 'Febrero', 'Marzo', 'Abril'],
    axisLine: { lineStyle: { color: 'white' } },
    axisLabel: { color: 'white' },
    name: 'Meses',
    nameTextStyle: { color: 'white' }
  },
  yAxis: {
    type: 'value',
    min: 30,
    max: 60,
    axisLine: { lineStyle: { color: 'white' } },
    axisLabel: { color: 'white' },
    name: 'Retención (%)',
    nameTextStyle: { color: 'white' }
  },
  series: [
    {
      name: 'Retención de Usuarios (%)',
      type: 'line',
      data: [35, 40, 45, 50],
      smooth: true,
      lineStyle: { color: '#4CAF50' },
      itemStyle: { color: '#4CAF50' },
      areaStyle: { color: 'rgba(76, 175, 80, 0.2)' }
    }
  ]
}

const resizeChart = () => {
  if (chartInstance) {
    chartInstance.resize()
  }
}

onMounted(async () => {
  await nextTick()
  // Esperamos a que el layout esté completamente montado
  setTimeout(() => {
    if (chartRef.value) {
      chartInstance = echarts.init(chartRef.value)
      chartInstance.setOption(option)
      window.addEventListener('resize', resizeChart)
    }
  }, 300)
})

onBeforeUnmount(() => {
  if (chartInstance) {
    chartInstance.dispose()
    chartInstance = null
  }
  window.removeEventListener('resize', resizeChart)
})
</script>

<style scoped>
.chart-container {
  width: 100%;
  height: 100%;
  min-height: 250px;
  background-color: #1e1e1e;
  border-radius: 6px;
}
</style>
