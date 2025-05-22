<template>
  <div class="chart-container">
    <canvas ref="chartRef"></canvas>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted, onBeforeUnmount, nextTick } from 'vue'
import {
  Chart,
  registerables,
  type ChartOptions,
  type ChartData
} from 'chart.js'

Chart.register(...registerables)

const chartRef = ref<HTMLCanvasElement | null>(null)
let chartInstance: Chart | null = null

const chartData: ChartData<'bar'> = {
  labels: ['Enero', 'Febrero', 'Marzo', 'Abril'],
  datasets: [
    {
      label: 'Usuarios Activos Diarios (DAU)',
      data: [20000, 24000, 28000, 32000],
      backgroundColor: '#00E396',
      borderRadius: 4,
    }
  ]
}

const chartOptions: ChartOptions<'bar'> = {
  responsive: true,
  maintainAspectRatio: false,
  plugins: {
    title: {
      display: true,
      text: 'Crecimiento de DAU',
      color: '#fff',
      font: {
        size: 18
      }
    },
    legend: {
      labels: {
        color: '#fff'
      }
    },
    tooltip: {
      callbacks: {
        label: ctx => `${(ctx.raw as number).toLocaleString()} usuarios`
      }
    }
  },
  scales: {
    x: {
      title: {
        display: true,
        text: 'Meses',
        color: '#aaa'
      },
      ticks: {
        color: '#fff'
      },
      grid: {
        color: '#333'
      }
    },
    y: {
      title: {
        display: true,
        text: 'Usuarios Diarios',
        color: '#aaa'
      },
      min: 0,
      max: 40000,
      ticks: {
        stepSize: 5000,
        color: '#fff',
        callback: val => Number(val).toLocaleString()
      },
      grid: {
        color: '#333'
      }
    }
  }
}

const renderChart = () => {
  if (chartRef.value) {
    chartInstance = new Chart(chartRef.value, {
      type: 'bar',
      data: chartData,
      options: chartOptions
    })
  }
}

onMounted(async () => {
  await nextTick()
  setTimeout(renderChart, 300)
})

onBeforeUnmount(() => {
  if (chartInstance) {
    chartInstance.destroy()
  }
})
</script>

<style scoped>
.chart-container {
  width: 100%;
  height: 100%;
  min-height: 350px;
  position: relative;
  background: #1E1E1E;
  padding: 10px;
  border-radius: 6px;
}
canvas {
  width: 100% !important;
  height: 100% !important;
}
</style>
