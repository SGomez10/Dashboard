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
   
   
        <ion-grid>
          <!-- Fila 1: Columna completa -->
          <ion-row>
            <ion-col size="12">
              <div class="box">Fila 1 - Completa</div>
            </ion-col>
          </ion-row>
   
   
          <!-- Fila 2: 3 columnas -->
          <ion-row>
            <ion-col size="12" size-lg="2">
              <div class="box">Columna 1</div>
            </ion-col>
            <ion-col size="12" size-lg="8">
              <div class="box">Columna 2</div>
            </ion-col>
            <ion-col size="12" size-lg="2">
              <div class="box">Columna 3</div>
            </ion-col>
          </ion-row>
   
   
          <!-- Fila 3: 4 cajas en 2 filas de 2 columnas -->
          <ion-row>
            <ion-col size="12" size-lg="6">
              <div class="box">Caja 1</div>
            </ion-col>
            <ion-col size="12" size-lg="6">
              <div class="box">Caja 2</div>
            </ion-col>
          </ion-row>
          <ion-row>
            <ion-col size="12" size-lg="6">
              <div class="box">Caja 3</div>
            </ion-col>
            <ion-col size="12" size-lg="6">
              <div class="box">Caja 4</div>
            </ion-col>
          </ion-row>
   
   
          <!--Fila 4: 6 cajas en una fila -->
          <ion-row>
            <ion-col size="12" size-lg="2" v-for="i in 6" :key="'sidebar-' + i">
              <div class="box">Sidebar {{ i }}</div>
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
    margin-bottom: 6px;
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
   </style>
   
   
   
   
   
   