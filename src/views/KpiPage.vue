<template>
    <ion-page>
      <ion-header :translucent="true">
        <ion-toolbar>
          <ion-buttons slot="start">
            <ion-menu-button color="primary"></ion-menu-button>
          </ion-buttons>
          <ion-title>🎯 KPIs</ion-title>
        </ion-toolbar>
      </ion-header>
  
  
      <ion-content :fullscreen="true" class="ion-padding">
        <ion-header collapse="condense">
          <ion-toolbar>
            <ion-title size="large">🎯 KPIs</ion-title>
          </ion-toolbar>
        </ion-header>
  
  
        <h1 class="ion-padding">🚀 KPIs de Negocio</h1>
        <ion-accordion-group expand="inset" :multiple="true">
          <ion-accordion value="1">
            <ion-item slot="header">
              <ion-label>Tasa de Retención a 7 Días</ion-label>
            </ion-item>
            <div class="ion-padding" slot="content">
                <p>Mejorar la retención de usuarios nuevos del 35% al 50% en los próximos 4 meses, implementando tutoriales interactivos y un sistema de recompensas por uso temprano,
                   para garantizar una base de usuarios más comprometida y aumentar los ingresos a largo plazo.</p>
                <h3>Objetivo SMART</h3>
                <p><strong>S</strong>: Mejorar la retención del 35% al 50%</p>
                <p><strong>M</strong>: 15 puntos porcentuales más</p>
                <p><strong>A</strong>: Tutoriales interactivos y recompensas</p>
                <p><strong>R</strong>: Usuarios retenidos generan más ingresos</p>
                <p><strong>T</strong>: En 4 meses</p>
            </div>
          </ion-accordion>
          <ion-accordion value="2">
            <ion-item slot="header">
              <ion-label>Ingresos por Usuario (ARPU)</ion-label>
            </ion-item>
            <div class="ion-padding" slot="content">
              <p>Incrementar los ingresos promedio por usuario en un 50% (de 0.50 a 0.75) durante los próximos 6 meses, lanzando funciones premium 
                y optimizando nuestro sistema de anuncios segmentados,
                con el objetivo de lograr una monetización más sostenible de la plataforma.</p>
              <h3>Objetivo SMART</h3>
              <p><strong>S</strong>: Incrementar el ARPU de 0.50 a 0.75</p>
              <p><strong>M</strong>: 50% más de ingresos por usuario</p>
              <p><strong>A</strong>: Introducción de features premium y anuncios segmentados</p>
              <p><strong>R</strong>: Monetización sostenible</p>
              <p><strong>T</strong>: En 6 meses</p>
            </div>
          </ion-accordion>
          <ion-accordion value="3">
            <ion-item slot="header">
              <ion-label>Porcentaje de publicaciones virales (likes/compartidos)</ion-label>
            </ion-item>
            <div class="ion-padding" slot="content">
              <p>Lograr que el 15% de las publicaciones alcancen más de 100 interacciones en los próximos 6 meses, mediante la implementación de challenges patrocinados
                 y mejoras en el algoritmo de recomendaciones, para aumentar el engagement orgánico y atraer nuevos usuarios a la plataforma.</p>
              <h3>Objetivo SMART</h3>
              <p><strong>S</strong>: Lograr que el 15% de las publicaciones sean virales</p>
              <p><strong>M</strong>: Meta clara (15% vs. línea base actual)</p>
              <p><strong>A</strong>: Challenges patrocinados y algoritmo de recomendación mejorado</p>
              <p><strong>R</strong>: Contenido viral atrae nuevos usuarios</p>
              <p><strong>T</strong>: En 6 meses.</p>
            </div>
          </ion-accordion>
          <ion-accordion value="4">
            <ion-item slot="header">
              <ion-label>Crecimiento de Usuarios Activos Diarios (DAU)</ion-label>
            </ion-item>
            <div class="ion-padding" slot="content">
              <p>Aumentar los usuarios diarios en un 50% (de 20,000 a 30,000) en los próximos 3 meses, 
                mediante campañas en redes sociales y notificaciones push personalizadas, 
                con el fin de fortalecer nuestra base de usuarios activos y aumentar el potencial de monetización</p>
              <h3>Objetivo SMART</h3>
              <p><strong>S</strong>: Aumentar los DAU de 20,000 a 30,000</p>
              <p><strong>M</strong>: 50% de crecimiento (10,000 usuarios nuevos)</p>
              <p><strong>A</strong>: Campañas en redes sociales y notificaciones push personalizadas</p>
              <p><strong>R</strong>: Más DAU = mayor potencial de monetización</p>
              <p><strong>T</strong>: En 3 meses.</p>
            </div>
          </ion-accordion>
          <ion-accordion value="5">
            <ion-item slot="header">
              <ion-label>Ratio de Viralidad (K-Factor)</ion-label>
            </ion-item>
            <div class="ion-padding" slot="content">
              <p>Alcanzar que cada usuario active invite a 1.5 personas en promedio durante los próximos 4 meses, a través de un programa de referidos con recompensas exclusivas, 
                con el fin de impulsar el crecimiento orgánico de nuestra base de usuarios sin incrementar los costos de adquisición.</p>
              <h3>Objetivo SMART</h3>
              <p><strong>S</strong>: Alcanzar un K-Factor de 1.5</p>
              <p><strong>M</strong>: Cada usuario invita a 1.5 personas en promedio</p>
              <p><strong>A</strong>: Programa de referidos con recompensas (ej: badges exclusivos).</p>
              <p><strong>R</strong>: Crecimiento orgánico sin coste adicional</p>
              <p><strong>T</strong>: En 4 meses.</p>
            </div>
          </ion-accordion>
        </ion-accordion-group>
        <br>
        <h1 class="ion-padding">📈 KPIs Técnicos</h1>
        <ion-accordion-group expand="inset" :multiple="true">
          <ion-accordion value="1">
            <ion-item slot="header" >
              <ion-label>Tiempo de Carga del Feed</ion-label>
            </ion-item>
            <div class="ion-padding" slot="content">
              <p>Reducir el tiempo de carga del feed en un 40% (de 2.5s a 1.5s) durante los próximos 2 meses, optimizando la compresión de imágenes
                 y mejorando nuestro sistema de caché, para ofrecer una experiencia de usuario más rápida y fluida que incremente la satisfacción y retención.</p>
              <h3>Objetivo SMART</h3>
              <p><strong>S</strong>: Reducir de 2.5s a 1.5s</p>
              <p><strong>M</strong>: 40% más rápido</p>
              <p><strong>A</strong>: Optimización de imágenes y caché</p>
              <p><strong>R</strong>: Mejor experiencia = mayor retención</p>
              <p><strong>T</strong>: En 2 meses.</p>
            </div>
          </ion-accordion>
          <ion-accordion value="2">
            <ion-item slot="header">
              <ion-label>Tasa de Errores en Subida de Contenido</ion-label>
            </ion-item>
            <div class="ion-padding" slot="content">
              <p>Disminuir la tasa de errores al subir contenido en un 80% (del 5% al 1%) en los próximos 3 meses, implementando mejores validaciones de formato y 
                tamaño de archivos, con el objetivo de reducir la frustración de los usuarios y mejorar su experiencia en la plataforma.</p>
              <h3>Objetivo SMART</h3>
              <p><strong>S</strong>: Disminuir del 5% al 1%</p>
              <p><strong>M</strong>: 80% menos errores</p>
              <p><strong>A</strong>: Validación mejorada de formatos y tamaño de archivos</p>
              <p><strong>R</strong>: Menor frustración para los usuarios</p>
              <p><strong>T</strong>: En 3 meses</p>
            </div>
          </ion-accordion>
          <ion-accordion value="3">
            <ion-item slot="header">
              <ion-label>Disponibilidad del Servidor </ion-label>
            </ion-item>
            <div class="ion-padding" slot="content">
              <p>Mantener la disponibilidad de la plataforma en un 99.95% mensual (máximo 22 minutos de inactividad) mediante la implementación de servidores redundantes en AWS, 
                para garantizar un servicio confiable y consistente que refuerce la credibilidad de nuestra aplicación además de evitar pérdidas de usuarios.</p>
              <h3>Objetivo SMART</h3>
              <p><strong>S</strong>: Mantener un uptime del 99.9%</p>
              <p><strong>M</strong>: 0.1% de tiempo de inactividad máximo</p>
              <p><strong>A</strong>: Monitoreo proactivo y redundancia de servidores</p>
              <p><strong>R</strong>: Evitar pérdidas de usuarios por caídas</p>
              <p><strong>T</strong>: Mensual (continuo)</p>
            </div>
          </ion-accordion>
          <ion-accordion value="4">
            <ion-item slot="header">
              <ion-label>Consumo de Batería</ion-label>
            </ion-item>
            <div class="ion-padding" slot="content">
              <p>Reducir el consumo de batería de la aplicación en un 50% durante los próximos 4 meses, optimizando los procesos en segundo plano,
                 con el fin de mejorar la experiencia de los usuarios con dispositivos menos potentes y prolongar su tiempo de uso.</p>
              <h3>Objetivo SMART</h3>
              <p><strong>S</strong>: Reducir el consumo del 20% al 10%</p>
              <p><strong>M</strong>: 50% menos consumo</p>
              <p><strong>A</strong>: Optimización de procesos en segundo plano</p>
              <p><strong>R</strong>: Mejorar la experiencia del usuario</p>
              <p><strong>T</strong>: En 4 meses.</p>
            </div>
          </ion-accordion>
          <ion-accordion value="5">
            <ion-item slot="header">
              <ion-label>Tiempo de Detección de Vulnerabilidades</ion-label>
            </ion-item>
            <div class="ion-padding" slot="content">
              <p></p>
              <h3>Objetivo SMART</h3>
              <p>Acortar el tiempo de detección de fallos críticos en un 85% (de 7 días a 1 día) durante los próximos 2 meses,
                 implementando herramientas de monitoreo automatizado como Sentry, para fortalecer la seguridad de nuestra plataforma
                 y proteger los datos de nuestros usuarios.</p>
              <p><strong>S</strong>: Reducir de 7 días a 1 día</p>
              <p><strong>M</strong>: 85% más rápido</p>
              <p><strong>A</strong>: Implementación de herramientas de monitoreo continuo como Sentry</p>
              <p><strong>R</strong>: Seguridad mejorada para los usuarios</p>
              <p><strong>T</strong>: En 2 meses</p>
            </div>
          </ion-accordion>
        </ion-accordion-group>
      </ion-content>
    </ion-page>
  </template>
  
  
  <script setup lang="ts">
  import { IonButtons, IonContent, IonHeader, IonMenuButton, IonPage, IonTitle, IonToolbar, IonAccordionGroup, IonAccordion, IonItem, IonLabel } from '@ionic/vue';
  </script>
  
  
  <style scoped>
  
  
  ion-accordion.accordion-collapsing ion-item[slot='header'],
    ion-accordion.accordion-collapsed ion-item[slot='header'] {
      --background: var(--ion-color-light);
      --color: var(--ion-color-light-contrast);
    }
  
  
    ion-accordion.accordion-expanding ion-item[slot='header'],
    ion-accordion.accordion-expanded ion-item[slot='header'] {
      --background: rgba(var(--ion-color-primary-rgb), 0.14);
      color: var(--ion-color-primary);
    }
  
  
  </style>