<template>
    <div class="chart-container">
      <apexchart
        ref="chartRef"
        width="100%"
        height="100%"
        type="line"
        :options="chartOptions"
        :series="series"
      />
    </div>
  </template>
  
  <script setup lang="ts">
  import { ref, onMounted, onBeforeUnmount } from 'vue'
  import ApexCharts from 'apexcharts'
  import ApexChart from 'vue3-apexcharts'
  
  const chartRef = ref()
  let interval: ReturnType<typeof setInterval>
  
  const series = ref<{ name: string; data: { x: number; y: number }[] }[]>([
      {
        name: 'Publicaciones virales (%)',
        data: [],
      },
    ])
  
  const chartOptions = ref({
    chart: {
      id: 'realtime-viral-chart',
      animations: {
        enabled: true,
        easing: 'linear',
        dynamicAnimation: {
          speed: 1000,
        },
      },
      toolbar: {
        show: false,
      },
      zoom: {
        enabled: false,
      },
    },
    stroke: {
      curve: 'smooth',
      width: 3,
    },
    xaxis: {
      type: 'datetime',
      labels: {
        datetimeFormatter: {
          hour: 'HH:mm:ss',
        },
      },
    },
    yaxis: {
      min: 0,
      max: 30,
      tickAmount: 6,
      title: {
        text: '% virales',
      },
    },
    title: {
      text: 'Evolución de publicaciones virales',
      align: 'center',
      style: {
        color: '#fff',
      },
    },
    grid: {
      borderColor: '#444',
    },
    theme: {
      mode: 'dark',
    },
    tooltip: {
      enabled: true,
    },
  })
  
  const generateFakeData = () => {
    const lastValue = series.value[0].data.slice(-1)[0]?.y || 5
    const nextValue = Math.min(
      30,
      Math.max(0, lastValue + (Math.random() * 4 - 2)) // Simula variaciones suaves
    )
    return {
      x: new Date().getTime(),
      y: parseFloat(nextValue.toFixed(2)),
    }
  }
  
  const updateChart = () => {
    const newPoint = generateFakeData()
    series.value[0].data.push(newPoint)
  
    // Limita la longitud del array
    if (series.value[0].data.length > 20) {
      series.value[0].data.shift()
    }
  }
  
  onMounted(() => {
    interval = setInterval(updateChart, 2000)
  })
  
  onBeforeUnmount(() => {
    clearInterval(interval)
  })
  </script>
  
  <style scoped>
  .chart-container {
    width: 100%;
    height: 100%;
    padding: 10px;
  }
  </style>
  