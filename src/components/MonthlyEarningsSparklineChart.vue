<template>
  <div v-if="showChart" class="chart-wrapper">
    <apexcharts
      ref="chartRef"
      type="line"
      height="100"
      :options="chartOptions"
      :series="series"
    />
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted, nextTick } from 'vue'
import ApexCharts from 'vue3-apexcharts'

const chartRef = ref<any>(null)
const showChart = ref(false)

// Datos de ejemplo: ganancias por mes
const series = [
  {
    name: 'Ganancias',
    data: [4200, 5100, 6700, 8200]
  }
]

// Opciones del gráfico sparkline
const chartOptions = {
  chart: {
    id: 'sparkline',
    type: 'line',
    sparkline: {
      enabled: true
    },
    animations: {
      enabled: true,
      easing: 'easeinout',
      speed: 800
    }
  },
  stroke: {
    curve: 'smooth',
    width: 2
  },
  tooltip: {
    enabled: true,
    y: {
      formatter: (val: number) => `€${val.toLocaleString()}`
    }
  },
  colors: ['#00E396'] // Verde para crecimiento
}

onMounted(async () => {
  setTimeout(async () => {
    showChart.value = true
    await nextTick()
    if (chartRef.value?.chart?.resize) {
      chartRef.value.chart.resize()
    }
  }, 100) // Espera breve para asegurar que el contenedor tiene tamaño
})
</script>

<style scoped>
.chart-wrapper {
  width: 100%;
  height: 100%;
  min-height: 100px;
}

.apexcharts-canvas {
  width: 100% !important;
  height: 100% !important;
  min-height: 100px !important;
}
</style>
