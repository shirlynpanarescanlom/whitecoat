<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <Header/>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true">
      <div class="bg-white rounded-lg my-4 mx-3 md:mx-auto md:w-md">
        <div class="bg-[#D9D9D9] p-2 rounded-t-lg mb-2 font-bold text-lg">
          <p>Doctor's Information</p>
        </div>
        <div class="px-2">
          <ion-label>Username:</ion-label>
          <ion-input class="bg-[#D9D9D9] rounded-md p-2"/>
        </div>
        <div class="px-2">
          <ion-label>Email</ion-label>
          <ion-input class="bg-[#D9D9D9] rounded-md p-2"/>
        </div>
        <div class="px-2 pb-2">
          <ion-label>Password</ion-label>
          <ion-input class="bg-[#D9D9D9] rounded-md p-2"/>
        </div>
      </div>
      <div class="my-4 mx-3 md:mx-auto flex justify-between items-center md:w-md gap-2">
        <ion-button fill="clear" class="w-full mb-4 border border-black font-bold transition duration-300 ease-in-out text-sm rounded-lg hover:bg-[#023E8A] hover:text-white text-[#023E8A]">
          Edit
        </ion-button>
        <ion-button fill="clear" class="w-full mb-4 border font-bold hover:bg-white hover:text-[#023E8A] hover:border-black hover:text-[#023E8A] transition duration-300 ease-in-out text-sm bg-[#023E8A] text-white rounded-lg">
          Update
        </ion-button>
      </div>
    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">
import { IonPage, IonHeader, IonToolbar, IonTitle, IonContent } from '@ionic/vue';
import Header from '@/components/Header.vue';
</script>

<style scoped>
ion-page{
    --background: #F0F0F0;
}
ion-toolbar{
    --background: #F0F0F0;
}
ion-content{
    --background: #F0F0F0;
} 
#form-container{
    background-color: white;
    padding: 20px;
    border-radius: 10px;
}#form-container form{
  background-color: #D9D9D9;
}
ion-input{
  --padding-start: 8px;
  --padding-end: 8px;
  --border-color: transparent;
}
ion-button{
  --padding-start: none;
  --padding-end: none;
}
</style>
