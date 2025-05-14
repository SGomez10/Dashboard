<template>
    <ion-page>
      <ion-header :translucent="true">
        <ion-toolbar>
          <ion-buttons slot="start">
            <ion-menu-button color="primary"></ion-menu-button>
          </ion-buttons>
          <ion-title>Dashboard</ion-title>
        </ion-toolbar>
      </ion-header>

      <ion-content :fullscreen="true" class="ion-padding">
        <ion-header collapse="condense">
          <ion-toolbar>
            <ion-title size="large">Dashboard</ion-title>
          </ion-toolbar>
        </ion-header>
   
        <ion-grid class="custom-dashboard">
          <!-- Fila 1: 2 columnas -->
          <ion-row>
            <ion-col size="12" size-lg="8">
              <div class="box">Col 1 - 8/12</div>
            </ion-col>
            <ion-col size="12" size-lg="4">
              <div class="box">Col 2 - 4/12</div>
            </ion-col>
          </ion-row>
   
   
          <!-- Fila 2: 4 columnas -->
          <ion-row>
            <ion-col size="12" size-md="6" size-lg="3" v-for="i in 4" :key="'fila2-'+i">
              <div class="box">Fila 2 - Col {{ i }}</div>
            </ion-col>
          </ion-row>
   
   
          <!-- Fila 3: 1 columna ancha -->
          <ion-row>
            <ion-col size="12">
              <div class="box tall">Fila 3 - Ancha</div>
            </ion-col>
          </ion-row>
   
   
          <!-- Fila 4: 5 columnas pequeñas -->
          <ion-row>
            <ion-col size="6" size-sm="4" size-md="2.4" v-for="i in 5" :key="'fila4-'+i">
              <div class="box">F4 - {{ i }}</div>
            </ion-col>
          </ion-row>
   
   
          <!-- Fila 5: 4 columnas iguales -->
          <ion-row>
            <ion-col size="6" size-md="3" v-for="i in 4" :key="'fila5-'+i">
              <div class="box">F5 - {{ i }}</div>
            </ion-col>
          </ion-row>
        </ion-grid>
      </ion-content>
    </ion-page>
   </template>
   
   
   <script setup lang="ts">
   import {
    IonButtons,
    IonContent,
    IonHeader,
    IonMenuButton,
    IonPage,
    IonTitle,
    IonToolbar,
    IonGrid,
    IonRow,
    IonCol
   } from '@ionic/vue';
   </script>
   
   
   <style scoped>
   ion-row {
    overflow: hidden;
    margin-bottom: 5px;
   }
   
   
   ion-col {
    --ion-grid-column-padding: 4px;
   }
   
   
   .box {
    background: #1E1E1E;
    color: white;
    border-radius: 8px;
    padding: 1rem;
    min-height: 80px;
    display: flex;
    justify-content: center;
    align-items: center;
    font-weight: bold;
    text-align: center;
   }
   
   
   .tall {
    min-height: 200px;
   }
   </style>