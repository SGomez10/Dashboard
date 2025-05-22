<template>
  <div ref="chartRef" class="echart-container"></div>
</template>

<script setup lang="ts">
import * as echarts from 'echarts'
import { ref, onMounted, onBeforeUnmount, nextTick } from 'vue'

const chartRef = ref<HTMLDivElement | null>(null)
let chartInstance: echarts.ECharts | null = null

const kFactorData = [1.0, 1.1, 1.2, 1.3, 1.4, 1.5]
const months = ['Noviembre', 'Diciembre', 'Enero', 'Febrero', 'Marzo', 'Abril']
const maxKFactor = 2.0

const initChart = () => {
  if (chartRef.value) {
    chartInstance = echarts.init(chartRef.value)

    const option = {
      title: {
        text: 'K-Factor - Radar',
        left: 'center',
        textStyle: { color: '#eee' },
      },
      tooltip: {
        trigger: 'item',
        formatter: (params: any) => {
          return `${params.seriesName}<br/>${params.name}: ${params.value}`
        },
      },
      radar: {
        indicator: months.map(m => ({ name: m, max: maxKFactor })),
        radius: '65%',
        splitNumber: 4,
        shape: 'circle',
        axisLine: { lineStyle: { color: '#555' } },
        splitLine: { lineStyle: { color: '#444' } },
        splitArea: { areaStyle: { color: 'transparent' } },
        name: { textStyle: { color: '#ccc', fontSize: 12 } },
      },
      series: [
        {
          name: 'K-Factor Mensual',
          type: 'radar',
          data: [
            {
              value: kFactorData,
              name: 'K-Factor',
              areaStyle: { color: 'rgba(0, 143, 251, 0.4)' },
              lineStyle: { color: '#008FFB', width: 3 },
              itemStyle: { color: '#008FFB' },
              symbolSize: 6,
            },
          ],
        },
      ],
    }

    chartInstance.setOption(option)
  }
}

const resizeChart = () => {
  if (chartInstance) {
    chartInstance.resize()
  }
}

onMounted(async () => {
  await nextTick()
  // Esperamos un poco más para asegurar que el ion-col tenga tamaño
  setTimeout(() => {
    initChart()
    resizeChart()
  }, 300)

  window.addEventListener('resize', resizeChart)
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
.echart-container {
  width: 100%;
  height: 100%;
  min-height: 300px;
  background-color: #1e1e1e;
  border-radius: 6px;
}
</style>
