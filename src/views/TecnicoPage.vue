<template>
  <ion-page>
    <ion-header :translucent="true">
      <ion-toolbar>
        <ion-buttons slot="start">
          <ion-menu-button color="primary"></ion-menu-button>
        </ion-buttons>
        <ion-title>Técnico</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content :fullscreen="true" class="ion-no-scroll ion-padding">
      <ion-grid class="main-grid">
        <!-- Fila 1 -->
        <ion-row class="grid-row">
          <ion-col size="12">
            <div class="box">
              <EChartWrapper 
                :options="performanceChartOptions as EChartsOption"
                height="100%"
              />
            </div>
          </ion-col>
        </ion-row>

        <!-- Fila 2 -->
        <ion-row class="grid-row">
          <ion-col size="12" size-lg="2">
            <div class="box">
              <ApexChartWrapper :options="uptimeChartOptions" />
            </div>
          </ion-col>
          <ion-col size="12" size-lg="8">
            <div class="box">
              <RealTimeChart 
                title="Tiempo de Respuesta API (ms)"
                :initial-data="[120, 125, 130]"
                :labels="['10:00', '10:05', '10:10']"
                style="height: 100%; width: 100%;"
              />
            </div>
          </ion-col>
          <ion-col size="12" size-lg="2">
            <div class="box">
              <CustomChart 
                title="Errores por Tipo"
                :data="[
                  { label: '500', value: 12, color: '#F44336' },
                  { label: '404', value: 8, color: '#FF9800' },
                  { label: '403', value: 3, color: '#FFEB3B' },
                  { label: 'Otros', value: 5, color: '#9E9E9E' }
                ]"
              />
            </div>
          </ion-col>
        </ion-row>

        <!-- Fila 3 -->
        <ion-row class="grid-row">
          <ion-col size="12" size-lg="6">
            <div class="box">
              <ChartJsWrapper 
                type="bar"
                :data="{
                  labels: ['<1s', '1-2s', '2-3s', '>3s'],
                  datasets: [{
                    label: 'Tiempos de Carga',
                    data: [85, 10, 3, 2],
                    backgroundColor: ['#4CAF50', '#FFC107', '#FF9800', '#F44336']
                  }]
                }"
                :options="{ responsive: true, plugins: { legend: { display: false } } }"
              />
            </div>
          </ion-col>
          <ion-col size="12" size-lg="6">
            <div class="box">
              <ChartJsWrapper 
                type="doughnut"
                :data="{
                  labels: ['200', '400', '500'],
                  datasets: [{
                    data: [92, 3, 5],
                    backgroundColor: ['#4CAF50', '#FFC107', '#F44336']
                  }]
                }"
                :options="{ responsive: true, plugins: { legend: { position: 'right' } } }"
              />
            </div>
          </ion-col>
        </ion-row>

        <!-- Fila 4 -->
        <ion-row class="grid-row">
          <ion-col size="12" size-lg="2" v-for="(chart, index) in miniCharts" :key="index">
            <div class="box">
              <ApexChartWrapper :options="chart" />
            </div>
          </ion-col>
        </ion-row>
      </ion-grid>
    </ion-content>
  </ion-page>
</template>


<script setup lang="ts">
import { ref, onMounted } from 'vue';
import { 
  IonPage, IonHeader, IonToolbar, IonTitle, IonContent, 
  IonButtons, IonMenuButton, IonGrid, IonRow, IonCol 
} from '@ionic/vue';
import CustomChart from '@/components/CustomChart.vue';
import ChartJsWrapper from '@/components/ChartJsWrapper.vue';
import ApexChartWrapper from '@/components/ApexChartWrapper.vue';
import EChartWrapper from '@/components/EChartWrapper.vue';
import RealTimeChart from '@/components/RealTimeChart.vue';
import type { ApexOptions } from 'apexcharts';
import type { EChartsOption } from 'echarts';

// Definimos las opciones del gráfico
const performanceChartOptions = ref<EChartsOption>({
  title: {
    text: 'Rendimiento del Sistema',
    subtext: 'CPU, Memoria y Disco',
    left: 'center',
    textStyle: { 
      color: '#fff', 
      fontSize: 16, 
      fontWeight: 'bold' 
    },
    subtextStyle: {
      color: '#fff', 
      fontSize: 12
    }
  },
  tooltip: {
    trigger: 'axis',
    axisPointer: {
      type: 'shadow'
    }
  },
  legend: {
    data: ['CPU', 'Memoria', 'Disco'],
    textStyle: {
      color: '#fff',
      fontSize: 12
    },
    top: '10%',
    right: '10%'
  },
  xAxis: {
    type: 'category',
    data: ['Enero', 'Febrero', 'Marzo', 'Abril', 'Mayo', 'Junio'],
    axisLabel: {
      color: '#fff'
    },
    axisLine: {
      lineStyle: {
        color: '#fff'
      }
    }
  },
  yAxis: {
    type: 'value',
    axisLabel: {
      color: '#fff'
    },
    axisLine: {
      lineStyle: {
        color: '#fff'
      }
    }
  },
  series: [
    {
      name: 'CPU',
      type: 'bar',
      data: [15, 22, 35, 40, 50, 60],
      itemStyle: {
        color: '#ff6347'
      }
    },
    {
      name: 'Memoria',
      type: 'bar',
      data: [30, 25, 40, 55, 60, 70],
      itemStyle: {
        color: '#4682b4'
      }
    },
    {
      name: 'Disco',
      type: 'bar',
      data: [40, 45, 60, 70, 80, 90],
      itemStyle: {
        color: '#32cd32'
      }
    }
  ]
});
const uptimeChartOptions = ref<ApexOptions>({
  chart: {
    type: 'radialBar',
    height: 200,
    background: '#1E1E1E'
  },
  plotOptions: {
    radialBar: {
      startAngle: -135,
      endAngle: 135,
      hollow: { margin: 0, size: '70%' },
      dataLabels: {
        name: { 
          offsetY: -10, 
          color: '#fff', 
          fontSize: '13px',
          fontWeight: 'bold'
        },
        value: { 
          color: '#fff', 
          fontSize: '20px', 
          offsetY: 10,
          fontWeight: 'bold',
          formatter: (val) => val + '%'
        }
      },
      track: { 
        background: '#333', 
        strokeWidth: '97%', 
        margin: 5,
        dropShadow: {
          enabled: true,
          top: 2,
          left: 0,
          blur: 4,
          opacity: 0.15
        }
      }
    }
  },
  fill: {
    type: 'gradient',
    gradient: {
      shade: 'dark',
      shadeIntensity: 0.15,
      inverseColors: false,
      stops: [0, 50, 65, 91],
      colorStops: [
        {
          offset: 0,
          color: '#00E396',
          opacity: 1
        },
        {
          offset: 100,
          color: '#008FFB',
          opacity: 1
        }
      ]
    }
  },
  stroke: { 
    dashArray: 4,
    lineCap: 'round'
  },
  labels: ['Uptime'],
  series: [99.95]
});

const miniCharts = ref<ApexOptions[]>([
  {
    chart: { 
      type: 'pie', // <-- Si quieres donut, pon 'donut'
      height: 150,
      background: '#1E1E1E'
    },
    labels: ['Éxito', 'Error'],
    series: [95, 5],
    colors: ['#4CAF50', '#F44336'],
    legend: { show: false },
    dataLabels: { enabled: false }
  },
  {
    chart: { 
      type: 'radialBar', 
      height: 150,
      background: '#1E1E1E'
    },
    plotOptions: {
      radialBar: {
        hollow: { size: '60%' },
        dataLabels: {
          name: { show: false },
          value: { 
            color: '#fff',
            fontSize: '16px',
            offsetY: 5,
            formatter: (val) => val + 'ms'
          }
        }
      }
    },
    series: [142],
    labels: ['Latencia'],
    colors: ['#2196F3']
  },
  {
    chart: { 
      type: 'bar', 
      height: 150,
      background: '#1E1E1E'
    },
    plotOptions: { 
      bar: { 
        horizontal: true,
        borderRadius: 4,
        barHeight: '80%'
      } 
    },
    series: [{ data: [78] }],
    colors: ['#FFC107'],
    xaxis: { 
      categories: ['Cache Hit'],
      labels: {
        style: {
          colors: ['#fff']
        }
      }
    },
    yaxis: {
      labels: {
        style: {
          colors: ['#fff']
        }
      }
    }
  },
  {
    chart: { 
      type: 'donut', 
      height: 150,
      background: '#1E1E1E'
    },
    labels: ['Mobile', 'Desktop', 'Tablet'],
    series: [45, 50, 5],
    colors: ['#9C27B0', '#3F51B5', '#009688'],
    legend: {
      labels: {
        colors: ['#fff']
      }
    }
  },
  {
    chart: { 
      type: 'line', 
      height: 150, 
      sparkline: { enabled: true },
      background: '#1E1E1E'
    },
    series: [{ data: [30, 40, 35, 50, 49, 60] }],
    colors: ['#4CAF50'],
    stroke: { curve: 'smooth', width: 3 },
    markers: {
      size: 5,
      colors: ['#4CAF50'],
      strokeWidth: 0
    }
  },
  {
    chart: { 
      type: 'area', 
      height: 150,
      background: '#1E1E1E'
    },
    series: [{ data: [30, 40, 35, 50, 49, 60] }],
    colors: ['#FF5722'],
    fill: { 
      type: 'gradient',
      gradient: {
        shadeIntensity: 1,
        opacityFrom: 0.7,
        opacityTo: 0.1,
        stops: [0, 100]
      }
    },
    stroke: { curve: 'smooth', width: 3 }
  }
]);
</script>

<style scoped>
html, body {
  height: 100%;
  overflow: hidden;
}

ion-page {
  display: flex;
  flex-direction: column;
  height: 100%;
}

ion-content {
  flex: 1;
  padding: 0;
  overflow: hidden;
}

.main-grid {
  height: 100%;
  display: flex;
  flex-direction: column;
}

/* Cada fila ocupa el mismo espacio en escritorio */
.grid-row {
  flex: 1;
  display: flex;
  flex-wrap: nowrap;
  min-height: 0;
  overflow: hidden;
  gap: 6px;
}

ion-col {
  display: flex;
  flex-direction: column;
  --ion-grid-column-padding: 4px;
  min-height: 0;
}

.box {
  background: #1E1E1E;
  color: white;
  border-radius: 8px;
  padding: 0.5rem;
  flex: 1;
  display: flex;
  justify-content: center;
  align-items: center;
  overflow: hidden;
  height: 100%;
  min-height: 0;
}

/* ⬇️ Cambios para modo móvil */
@media (max-width: 768px) {
  ion-content {
    overflow-y: auto; /* permite scroll en móvil */
  }

  .main-grid {
    height: auto;
    min-height: 100%;
  }

  .grid-row {
    flex-direction: column;
    flex: none;
    min-height: auto;
    margin-bottom: 12px;
  }

  ion-col {
    height: auto;
  }

  .box {
    height: auto;
    min-height: 200px; /* altura mínima razonable para gráficos en mobile */
  }
}
</style>
