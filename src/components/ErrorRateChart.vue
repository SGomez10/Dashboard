<template>
  <div ref="chartRef" class="chart-container" />
</template>

<script setup lang="ts">
import * as echarts from 'echarts';
import { ref, onMounted, onBeforeUnmount, nextTick } from 'vue';

const chartRef = ref<HTMLElement | null>(null);
let chart: echarts.ECharts | null = null;
let resizeObserver: ResizeObserver;

onMounted(async () => {
  await nextTick(); // espera a que el DOM esté completamente renderizado

  if (chartRef.value) {
    chart = echarts.init(chartRef.value);

    chart.setOption({
      title: {
        text: 'Distribución de errores por tamaño y duración de carga',
        left: 'center',
        textStyle: { color: '#fff' }
      },
      tooltip: {
        trigger: 'item',
        formatter: (params:any) =>
          `Tamaño: ${params.value[0]}MB<br/>Duración: ${params.value[1]}s<br/>Errores: ${params.value[2]}`
      },
      xAxis: {
        name: 'Tamaño del archivo (MB)',
        nameTextStyle: { color: '#fff' },
        axisLabel: { color: '#ccc' },
        splitLine: { lineStyle: { color: '#444' } }
      },
      yAxis: {
        name: 'Duración de carga (s)',
        nameTextStyle: { color: '#fff' },
        axisLabel: { color: '#ccc' },
        splitLine: { lineStyle: { color: '#444' } }
      },
      series: [
        {
          name: 'Errores',
          type: 'scatter',
          symbolSize: (val:any) => val[2] * 4,
          data: [
            [1.2, 4.5, 1],
            [2.5, 6.8, 3],
            [3.1, 7.2, 5],
            [0.9, 2.8, 0],
            [4.0, 10.1, 7],
            [1.8, 3.5, 1],
            [2.7, 5.9, 2],
            [3.5, 6.3, 4],
            [4.5, 12.0, 6],
            [5.0, 13.5, 8]
          ],
          emphasis: {
            focus: 'series'
          },
          itemStyle: {
            color: '#FF6B6B'
          }
        }
      ]
    });

    // Observa el tamaño del contenedor
    resizeObserver = new ResizeObserver(() => {
      if (chart) {
        chart.resize();
      }
    });

    resizeObserver.observe(chartRef.value);
  }
});

onBeforeUnmount(() => {
  if (resizeObserver && chartRef.value) {
    resizeObserver.unobserve(chartRef.value);
  }
  if (chart) {
    chart.dispose();
  }
});
</script>

<style scoped>
.chart-container {
  width: 100%;
  height: 100%;
}
</style>
