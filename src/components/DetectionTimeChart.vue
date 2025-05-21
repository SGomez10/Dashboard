<template>
    <div class="chart-container">
      <apexchart
        ref="chartRef"
        :key="chartKey"
        width="100%"
        height="100%"
        type="candlestick"
        :options="chartOptions"
        :series="series"
      />
    </div>
  </template>
  
  <script setup lang="ts">
  import { ref, onMounted, nextTick } from 'vue'
  import ApexCharts from 'apexcharts'
  import VueApexCharts from 'vue3-apexcharts'
  
  const chartRef = ref()
  const chartKey = ref(0)
  
  onMounted(() => {
    // Asegura que el DOM esté listo y se pueda calcular correctamente el tamaño
    nextTick(() => {
      setTimeout(() => {
        chartKey.value++
        if (chartRef.value?.chart?.resize) {
          chartRef.value.chart.resize()
        }
      }, 200)
    })
  })
  
  // Datos inventados que simulan el tiempo de detección de fallos críticos
  const series = [
    {
      data: [
        {
          x: 'Semana 1',
          y: [7, 6.5, 6.8, 6.2],
        },
        {
          x: 'Semana 2',
          y: [6.2, 5.8, 6, 5.5],
        },
        {
          x: 'Semana 3',
          y: [5.5, 4.5, 5, 4.2],
        },
        {
          x: 'Semana 4',
          y: [4.2, 3.5, 3.8, 3.1],
        },
        {
          x: 'Semana 5',
          y: [3.1, 2.5, 2.8, 2.2],
        },
        {
          x: 'Semana 6',
          y: [2.2, 1.5, 1.8, 1],
        },
        {
          x: 'Semana 7',
          y: [1, 1.2, 1.1, 1],
        },
      ],
    },
  ]
  
  const chartOptions = {
    chart: {
      type: 'candlestick',
      toolbar: {
        show: false,
      },
      animations: {
        enabled: true,
      },
    },
    title: {
      text: 'Detección de Fallos Críticos (días)',
      align: 'left',
      style: {
        color: '#ffffff',
        fontSize: '16px',
      },
    },
    xaxis: {
      type: 'category',
      labels: {
        style: {
          colors: '#ffffff',
        },
      },
    },
    yaxis: {
      tooltip: {
        enabled: true,
      },
      labels: {
        style: {
          colors: '#ffffff',
        },
      },
    },
    theme: {
      mode: 'dark',
    },
  }
  </script>
  
  <style scoped>
  .chart-container {
    width: 100%;
    height: 100%;
    padding: 1rem;
    box-sizing: border-box;
  }
  </style>
  