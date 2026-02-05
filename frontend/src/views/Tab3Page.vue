<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <Header/>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true">
      <div class=" w-full max-w-md mx-auto my-5 bg-gray-200 flex items-center justify-start
      ">
        <form action="">
          <label for="name">Name:</label>
          <ion-input id="name" name="name" placeholder="Full name" class="w-full"></ion-input>

          <label for="age" class="mt-2">Age:</label>
          <ion-input id="age" name="age" type="number" placeholder="Age"></ion-input>

          <label for="gender" class="mt-2">Gender:</label>
          <ion-input id="gender" name="gender" placeholder="Gender"></ion-input>

          <label for="address" class="mt-2">Address:</label>
          <ion-input id="address" name="address" placeholder="Address"></ion-input>

          <label for="contact" class="mt-2">Contact:</label>
          <ion-input id="contact" name="contact" type="tel" placeholder="Phone number"></ion-input>

          <label for="email" class="mt-2">Email:</label>
          <ion-input id="email" name="email" type="email" placeholder="Email"></ion-input>

          <label for="medicalId" class="mt-2">Medical ID:</label>
          <ion-input id="medicalId" name="medicalId" placeholder="Medical ID"></ion-input>

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
ion-page{
    --background: #F0F0F0;
}
ion-header{
    --background: #F0F0F0;
}
ion-content{
    --background: #F0F0F0;
}
</style>
