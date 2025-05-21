<template>
    <div class="chart-container">
      <apexcharts
        ref="chartRef"
        type="bar"
        :options="chartOptions"
        :series="series"
        height="350"
        width="100%"
      />
    </div>
  </template>
  
  <script setup lang="ts">
  import { ref, onMounted, nextTick } from 'vue'
  import ApexCharts from 'apexcharts'
  import ApexChart from 'vue3-apexcharts'
  
  // Ref con tipo any para evitar error TS
  const chartRef = ref<any>(null)
  
  const series = [
    {
      name: 'Ingresos Promedio por Usuario',
      data: [0.50, 0.55, 0.60, 0.65, 0.70, 0.75], // valores ejemplo progresivos en 6 meses
    },
  ]
  
  const chartOptions = {
    chart: {
      id: 'arpu-bar',
      toolbar: {
        show: false,
      },
      animations: {
        enabled: true,
        easing: 'easeinout',
        speed: 800,
      },
    },
    xaxis: {
      categories: ['Mes 1', 'Mes 2', 'Mes 3', 'Mes 4', 'Mes 5', 'Mes 6'],
      title: {
        text: 'Tiempo (Meses)',
      },
    },
    yaxis: {
      min: 0,
      max: 1,
      tickAmount: 5,
      title: {
        text: 'Ingresos Promedio ($)',
      },
    },
    tooltip: {
      enabled: true,
      y: {
        formatter: (val: number) => `$${val.toFixed(2)}`,
      },
    },
    colors: ['#008FFB'],
    dataLabels: {
      enabled: true,
      formatter: (val: number) => `$${val.toFixed(2)}`,
    },
  }
  
  onMounted(async () => {
    // Esperamos el siguiente tick para asegurarnos que el DOM está listo
    await nextTick()
  
    // Forzamos el resize para evitar problemas de renderizado inicial
    if (
      chartRef.value &&
      chartRef.value.chart &&
      typeof chartRef.value.chart.resize === 'function'
    ) {
      chartRef.value.chart.resize()
    }
  })
  </script>
  
  <style scoped>
  .chart-container {
    width: 100%;
    height: 100%;
  }
  </style>
  