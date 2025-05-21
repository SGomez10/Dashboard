<template>
  <div class="chart-container">
    <!-- Solo renderiza el gráfico cuando el componente está listo -->
    <apexchart
      v-if="isReady"
      type="line"
      height="100%"
      width="100%"
      :options="chartOptions"
      :series="series"
    />
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import ApexCharts from 'apexcharts'
import VueApexCharts from 'vue3-apexcharts'

// Registro del componente si no se ha hecho globalmente
// (si ya lo registraste en main.ts, puedes omitir esto)
defineProps()
defineEmits()
const isReady = ref(false)

const chartOptions = {
  chart: {
    id: 'server-uptime',
    animations: {
      enabled: true
    },
    toolbar: {
      show: false
    },
    zoom: {
      enabled: false
    },
    background: 'transparent'
  },
  title: {
    text: 'Disponibilidad mensual del servidor',
    align: 'center',
    style: {
      color: '#ffffff',
      fontSize: '16px'
    }
  },
  xaxis: {
    categories: ['Ene', 'Feb', 'Mar', 'Abr', 'May'],
    labels: {
      style: { colors: '#ffffff' }
    }
  },
  yaxis: {
    min: 99.8,
    max: 100,
    tickAmount: 5,
    labels: {
      formatter: val => `${val.toFixed(2)}%`,
      style: { colors: '#ffffff' }
    }
  },
  grid: {
    borderColor: '#444',
    strokeDashArray: 4
  },
  stroke: {
    curve: 'smooth',
    width: 2
  },
  markers: {
    size: 4,
    colors: ['#00e396']
  },
  colors: ['#00e396'],
  theme: {
    mode: 'dark'
  },
  tooltip: {
    theme: 'dark',
    y: {
      formatter: val => `${val.toFixed(2)}%`
    }
  }
}

const series = [
  {
    name: 'Uptime',
    data: [99.94, 99.96, 99.92, 99.95, 99.97]
  }
]

onMounted(() => {
  // Forzar render una vez montado
  setTimeout(() => {
    isReady.value = true
  }, 100)
})
</script>

<style scoped>
.chart-container {
  width: 100%;
  height: 100%;
  padding: 10px;
  box-sizing: border-box;
}
</style>
