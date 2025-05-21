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


    <ion-content :fullscreen="true" class="ion-padding">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">Técnico</ion-title>
        </ion-toolbar>
      </ion-header>


      <!-- Grid principal del Dashboard -->
      <ion-grid class="dashboard-grid">
        <!--Fila 1: 4 Columnas -->
        <ion-row class="ion-row-1">
          <!--Columna 1 – Uptime Mensual -->
          <ion-col size="12" size-lg="4">
            <div class="box kpi-box">
              <div class="kpi-content">
                <h4>Uptime</h4>
                <p class="kpi-value">99.97%</p>
                <p class="kpi-subtext">Este mes</p>
              </div>
            </div>
          </ion-col>

          <!--Columna 2 – Errores de subida -->
          <ion-col size="6" size-lg="4">
            <div class="box kpi-box">
              <div class="kpi-content">
                <h4>Errores de subida</h4>
                <p class="kpi-value">23 errores</p>
                <p class="kpi-subtext">Últimos 30 días</p>
              </div>
            </div>
          </ion-col>

          <!--Columna 3 – Tiempo medio de carga -->
          <ion-col size="6" size-lg="4">
            <div class="box kpi-box">
              <div class="kpi-content">
                <h4>Tiempo medio</h4>
                <p class="kpi-value">3.2s</p>
                <p class="kpi-subtext">por archivo</p>
              </div>
            </div>
          </ion-col>
        </ion-row>


        <!-- 🔵 Fila 2: 2 Columnas -->
        <ion-row class="ion-row-2">
          <ion-col size="12" size-md="3" push-md="9">
            <div class="box"><FeedLoadTImeChart/></div>
          </ion-col>
            <ion-col size="12" size-md="9" pull-md="3">
              <div class="box"><BatteryChart/></div>
            </ion-col>
        </ion-row>


        <!-- 🟠 Fila 3: 2 Columnas -->
        <ion-row class="ion-row-3">
          <ion-col size="12" size-lg="4.5">
            <div class="box"><ServerUptimeChart/></div>
          </ion-col>
          <ion-col size="12" size-lg="4.5">
            <div class="box"><ErrorRateChart/></div>
          </ion-col>
          <ion-col size="12" size-lg="3">
            <div class="box"><DetectionTimeChart/></div>
          </ion-col>
        </ion-row>
      </ion-grid>
    </ion-content>
  </ion-page>
</template>


<script setup lang="ts">
import { IonButtons, IonContent, IonHeader, IonMenuButton, IonPage, IonTitle, IonToolbar, IonGrid, IonRow, IonCol } from '@ionic/vue';
import BatteryChart from '@/components/BatteryChart.vue';
import ServerUptimeChart from '@/components/ServerUptimeChart.vue';
import ErrorRateChart from '@/components/ErrorRateChart.vue';
import DetectionTimeChart from '@/components/DetectionTimeChart.vue';
import FeedLoadTImeChart from '@/components/FeedLoadTImeChart.vue';

</script>


<style scoped>


ion-row{
  overflow: hidden;
}


ion-col {
  max-height: 100%;
  --ion-grid-column-padding:10px;
}


/* El contenido real de cada columna */
.box {
  background: #1E1E1E;
  height: 100%;
  max-height: 100%;
  overflow: hidden;
  border-radius:5px;
  display: flex;
  justify-content: center;
  align-items: start;
}

canvas {
  width: 100% !important;
  height: 100% !important;
}

.kpi-box {
  flex-direction: column;
  align-items: center;
  justify-content: center;
  text-align: center;
  padding: 1rem;
}

.kpi-content h4 {
  margin: 0;
  font-size: 1.1rem;
  color: #90e0ef;
}

.kpi-value {
  font-size: 2rem;
  font-weight: bold;
  margin: 0.5rem 0;
  color: #ffffff;
}

.kpi-subtext {
  font-size: 0.9rem;
  color: #ccc;
}


/* Aplicar altura total y por filas, solo en pantallas ≥ md */
@media (min-width: 992px) {  
  ion-grid{height: 100%;}
  .ion-row-1{height: 20%; max-height: 20%;}
  .ion-row-2{height: 40%; max-height: 40%;}
  .ion-row-3{height: 40%; max-height: 40%;}
}


</style>