<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <Header/>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true">
      <div class="flex items-center justify-center mt-2">
      <ion-searchbar fill="clear" placeholder="Search patient..." class="px-2 w-full max-w-md md:mt-4"></ion-searchbar>
      </div>
      <div class="px-2 mb-2 flex flex-col justify-center items-center ">
        <div class="flex items-center justify-between w-full max-w-md mb-4">
          <p class="font-light text-xl text-gray-800">Prescribe</p>
          <font-awesome-icon :icon="['fas', 'circle-arrow-right']" class="text-3xl mt-2 text-gray-600 cursor-pointer hover:opacity-75"/>
        </div>
        <div class="mt-4 h-100 bg-[#D9D9D9] py-3 w-full max-w-md px-2 rounded-sm flex flex-col items-center justify-center">
          <p class="text-center">No history...</p>
        </div>
      </div>


    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">
import { IonPage, IonHeader, IonToolbar, IonContent, IonIcon } from '@ionic/vue';
import Header from '../components/header.vue';
</script>

<style scoped>
ion-page, ion-header, ion-toolbar, ion-content {
    --background: #F0F0F0;
    --color: #000000;
}
ion-searchbar {
  --box-shadow: none;
  --background: #D9D9D9;
  --color: #000000;
  --border-radius: 9999px;
}
</style>
