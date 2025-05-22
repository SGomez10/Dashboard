<template>
  <ion-page>
    <ion-header :translucent="true">
      <ion-toolbar>
        <ion-buttons slot="start">
          <ion-menu-button color="primary"></ion-menu-button>
        </ion-buttons>
        <ion-title>Negocio</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content :fullscreen="true" class="ion-padding">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">Negocio</ion-title>
        </ion-toolbar>
      </ion-header>

      <ion-grid class="dashboard-grid">
        <!-- Fila 1 -->
        <ion-row class="ion-row-1">
          <!-- Retención de usuarios -->
          <ion-col size="6" size-lg="3">
            <div class="box kpi-box">
              <div class="kpi-content">
                <h4>Retención mensual</h4>
                <p class="kpi-value">72%</p>
                <p class="kpi-subtext">Usuarios que regresan</p>
              </div>
            </div>
          </ion-col>

          <!-- Ganancias del mes -->
          <ion-col size="6" size-lg="3">
            <div class="box kpi-box">
              <div class="kpi-content">
                <h4>Ingresos</h4>
                <p class="kpi-value">€8,200</p>
                <p class="kpi-subtext">Este mes</p>
              </div>
            </div>
          </ion-col>

          <!-- Contenido viral generado -->
          <ion-col size="6" size-lg="3">
            <div class="box kpi-box">
              <div class="kpi-content">
                <h4>Contenido viral</h4>
                <p class="kpi-value">378 posts</p>
                <p class="kpi-subtext">Últimos 30 días</p>
              </div>
            </div>
          </ion-col>

          <!-- Usuarios activos diarios -->
          <ion-col size="6" size-lg="3">
            <div class="box kpi-box">
              <div class="kpi-content">
                <h4>Usuarios activos</h4>
                <p class="kpi-value">4,570</p>
                <p class="kpi-subtext">DAU promedio</p>
              </div>
            </div>
          </ion-col>
        </ion-row>

        <!-- Fila 2 -->
        <ion-row class="ion-row-2">
          <ion-col size="12" size-lg="9">
            <div class="box"><UserRetentionChart /> </div>
          </ion-col>
          <ion-col size="12" size-lg="3">
            <div class="box"> <KFactorChart/></div>
          </ion-col>
        </ion-row>

        <!-- Fila 3 -->
        <ion-row class="ion-row-3">
          <ion-col size="12" size-lg="6">
            <div class="box"> <ViralPostChart/> </div>
          </ion-col>
          <ion-col size="12" size-lg="6">
            <div class="box"> <DAUChart/> </div>
          </ion-col>
        </ion-row>
      </ion-grid>
    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">
import { IonButtons, IonContent, IonHeader, IonMenuButton, IonPage, IonTitle, IonToolbar, IonGrid, IonRow, IonCol } from '@ionic/vue'
import UserRetentionChart from '@/components/UserRetentionChart.vue';
import ARPUChart from '@/components/ARPUChart.vue';
import KFactorChart from '@/components/KFactorChart.vue';
import ViralPostChart from '@/components/ViralPostChart.vue';
import DAUChart from '@/components/DAUChart.vue';
import MonthlyEarningsSparklineChart from '@/components/MonthlyEarningsSparklineChart.vue';
</script>

<style scoped>
ion-row {
  overflow: hidden;
}

ion-col {
  max-height: 100%;
  --ion-grid-column-padding: 10px;
}

.box {
  background: #1E1E1E;
  height: 100%;
  max-height: 100%;
  overflow: hidden;
  border-radius: 5px;
  display: flex;
  justify-content: center;
  align-items: center;
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

@media (min-width: 992px) {
  ion-grid { height: 100%; }
  .ion-row-1 { height: 20%; max-height: 20%; }
  .ion-row-2 { height: 40%; max-height: 40%; }
  .ion-row-3 { height: 40%; max-height: 40%; }
}
</style>
