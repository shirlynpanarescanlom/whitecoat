<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <Header/>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true">
      <div class="px-2 flex flex-col justify-center items-center ">
        <ion-searchbar fill="clear" placeholder="Search patient..." class="w-full max-w-md mt-3 md:mt-4 rounded-full bg-[#D9D9D9]"></ion-searchbar>
        <div class="flex items-center justify-between w-full max-w-md mt-2 mb-4 px-4">
          <p class="font-light text-2xl text-gray-800">Prescribe</p>
          <font-awesome-icon :icon="['fas', 'circle-arrow-right']" class="text-4xl mt-2 text-gray-600"/>
        </div>
        <div class=" mt-4 h-100 bg-[#D9D9D9] py-3 w-full md:w-md px-2 rounded-sm">
          <p class="text-center">No history...</p>
        </div>
      </div>


    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">
import { IonPage, IonHeader, IonToolbar, IonContent, IonIcon } from '@ionic/vue';
import Header from '@/components/Header.vue';
</script>

<style scoped>

ion-page{
    --background: #F0F0F0;
}
ion-toolbar{
    --background: #F0F0F0;
}
ion-header{
    --background: #F0F0F0;
}
ion-content{
    --background: #F0F0F0;
}
ion-searchbar {
  --box-shadow: none;
  --background: transparent;
}
</style>
