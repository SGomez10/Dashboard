<template>
    <apexchart
      type="line"
      height="300"
      :options="chartOptions"
      :series="series"
      :key="chartKey"
    />
  </template>
  
  <script setup>
  import { ref, onMounted, onBeforeUnmount } from 'vue'
  
  const chartKey = ref(0)
  
  const series = ref([{
    name: 'Tiempo de carga (s)',
    data: []
  }])
  
  const chartOptions = ref({
    chart: {
      id: 'realtime',
      animations: {
        enabled: true,
        easing: 'linear',
        dynamicAnimation: {
          speed: 1000
        }
      },
      toolbar: { show: false },
      zoom: { enabled: false }
    },
    stroke: {
      curve: 'smooth'
    },
    xaxis: {
      type: 'datetime',
      range: 20000
    },
    yaxis: {
      min: 1,
      max: 3,
      title: { text: 'Segundos' }
    },
    title: {
      text: 'Tiempo de carga del feed (en tiempo real)',
      align: 'center'
    }
  })
  
  let interval
  
  function generateDataPoint() {
    return {
      x: new Date().getTime(),
      y: parseFloat((Math.random() + 1.5).toFixed(2)) // entre 1.5 y 2.5
    }
  }
  
  onMounted(() => {
    const initial = Array.from({ length: 10 }, (_, i) => {
      return {
        x: new Date().getTime() - (10 - i) * 1000,
        y: generateDataPoint().y
      }
    })
  
    series.value[0].data = initial
  
    interval = setInterval(() => {
      const newPoint = generateDataPoint()
      const data = series.value[0].data
  
      data.push(newPoint)
      if (data.length > 20) data.shift()
      chartKey.value++ // forzar rerender
    }, 1000)
  })
  
  onBeforeUnmount(() => {
    clearInterval(interval)
  })
  </script>
  