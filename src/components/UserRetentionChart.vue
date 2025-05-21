<template>
    <div class="chart-container">
      <canvas ref="retentionChart"></canvas>
    </div>
  </template>
  
  <script setup lang="ts">
  import { onMounted, onBeforeUnmount, ref, nextTick } from 'vue'
  import {
    Chart,
    LineController,
    LineElement,
    PointElement,
    LinearScale,
    Title,
    CategoryScale,
    Tooltip,
    Filler
  } from 'chart.js'
  
  Chart.register(
    LineController,
    LineElement,
    PointElement,
    LinearScale,
    Title,
    CategoryScale,
    Tooltip,
    Filler
  )
  
  const chartRef = ref<HTMLCanvasElement | null>(null)
  let chartInstance: Chart | null = null
  
  const createChart = () => {
    if (!chartRef.value) return
  
    const ctx = chartRef.value.getContext('2d')
    if (!ctx) return
  
    chartInstance = new Chart(ctx, {
      type: 'line',
      data: {
        labels: ['Mes 1', 'Mes 2', 'Mes 3', 'Mes 4'],
        datasets: [
          {
            label: 'Retención de Usuarios (%)',
            data: [35, 40, 45, 50],
            borderColor: '#4CAF50',
            backgroundColor: 'rgba(76, 175, 80, 0.2)',
            fill: true,
            tension: 0.3,
            pointRadius: 5
          }
        ]
      },
      options: {
        responsive: true,
        maintainAspectRatio: false,
        scales: {
          y: {
            min: 30,
            max: 60,
            ticks: { color: 'white' },
            title: { display: true, text: 'Retención (%)', color: 'white' }
          },
          x: {
            ticks: { color: 'white' },
            title: { display: true, text: 'Meses', color: 'white' }
          }
        },
        plugins: {
          legend: {
            labels: { color: 'white' }
          },
          title: {
            display: true,
            text: 'Evolución de Retención de Usuarios Nuevos',
            color: 'white'
          }
        }
      }
    })
  }
  
  onMounted(async () => {
    await nextTick()
    setTimeout(() => {
      createChart()
    }, 200)
  })
  
  onBeforeUnmount(() => {
    chartInstance?.destroy()
  })
  </script>
  
  <style scoped>
  .chart-container {
    width: 100%;
    height: 100%;
    position: relative;
  }
  
  canvas {
    width: 100% !important;
    height: 100% !important;
  }
  </style>
  