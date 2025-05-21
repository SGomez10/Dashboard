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
          <ion-col size="6" size-lg="3">
            <div class="box">            </div>
          </ion-col>
          <ion-col size="6" size-lg="3">
            <div class="box">            </div>
          </ion-col>
          <ion-col size="6" size-lg="3">
            <div class="box">            </div>
          </ion-col>
          <ion-col size="6" size-lg="3">
            <div class="box">            </div>
          </ion-col>
        </ion-row>

        <!-- Fila 2 -->
        <ion-row class="ion-row-2">
          <ion-col size="12" size-lg="9">
            <div class="box"><UserRetentionChart /> </div>
          </ion-col>
          <ion-col size="12" size-lg="3">
            <div class="box">            </div>
          </ion-col>
        </ion-row>

        <!-- Fila 3 -->
        <ion-row class="ion-row-3">
          <ion-col size="12" size-lg="6">
            <div class="box">
              <p style="color:white;">Objetivos SMART resumen</p>
            </div>
          </ion-col>
          <ion-col size="12" size-lg="6">
            <div class="box">
              <p style="color:white;">Estado técnico</p>
            </div>
          </ion-col>
        </ion-row>
      </ion-grid>
    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">
import { IonButtons, IonContent, IonHeader, IonMenuButton, IonPage, IonTitle, IonToolbar, IonGrid, IonRow, IonCol } from '@ionic/vue'
import UserRetentionChart from '@/components/UserRetentionChart.vue';
// Components
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

@media (min-width: 992px) {
  ion-grid { height: 100%; }
  .ion-row-1 { height: 20%; max-height: 20%; }
  .ion-row-2 { height: 40%; max-height: 40%; }
  .ion-row-3 { height: 40%; max-height: 40%; }
}
</style>
