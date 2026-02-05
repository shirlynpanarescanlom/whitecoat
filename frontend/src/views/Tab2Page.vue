<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <Header/>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true">
      <div id="prescription-container" class="px-2 mt-4 my-4 mx-3 p-4 rounded-lg mx-2">
        <p>Prescription</p>
        <p>Digital prescription for a patient</p>
        <form action="">
          <label for="name">Name:</label>
          <input type="text" id="name" name="name" />
        </form>
      </div>
    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">
import { IonPage, IonHeader, IonToolbar, IonTitle, IonContent } from '@ionic/vue';
import ExploreContainer from '@/components/ExploreContainer.vue';
import Header from '@/components/Header.vue';
</script>

<style>
body{
  background-color: #F0F0F0;
}
#prescription-container{
  background-color: white;
}
</style>
