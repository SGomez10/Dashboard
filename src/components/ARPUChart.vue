<template>
  <div ref="containerRef" class="chart-container">
    <apexcharts
      ref="chartRef"
      type="bar"
      :options="chartOptions"
      :series="series"
      height="100%"
      width="100%"
    />
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted, nextTick } from 'vue'
import ApexCharts from 'apexcharts'
import apexcharts from 'vue3-apexcharts'

const chartRef = ref<any>(null)
const containerRef = ref<HTMLElement | null>(null)

const series = [
  {
    name: 'Ingresos Promedio por Usuario',
    data: [0.50, 0.55, 0.60, 0.65, 0.70, 0.75],
  },
]

const chartOptions = {
  chart: {
    id: 'arpu-bar',
    toolbar: { show: false },
    animations: {
      enabled: true,
      easing: 'easeinout',
      speed: 800,
    },
  },
  xaxis: {
    categories: ['Mes 1', 'Mes 2', 'Mes 3', 'Mes 4', 'Mes 5', 'Mes 6'],
    title: { text: 'Tiempo (Meses)' },
  },
  yaxis: {
    min: 0,
    max: 1,
    tickAmount: 5,
    title: { text: 'Ingresos Promedio ($)' },
  },
  tooltip: {
    enabled: true,
    y: {
      formatter: (val: any) => `$${val.toFixed(2)}`,
    },
  },
  colors: ['#008FFB'],
  dataLabels: {
    enabled: true,
    formatter: (val: any) => `$${val.toFixed(2)}`,
  },
}

onMounted(async () => {
  await nextTick()

  // Esperamos un breve tiempo para asegurar que el contenedor tenga dimensiones
  setTimeout(() => {
    if (chartRef.value?.chart?.resize) {
      chartRef.value.chart.resize()
    }
  }, 300)
})
</script>

<style scoped>
.chart-container {
  width: 100%;
  height: 100%;
  min-height: 350px;
}
</style>
