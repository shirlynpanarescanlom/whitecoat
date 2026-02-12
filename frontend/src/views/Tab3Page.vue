<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <Header/>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true">
      <div id="form-container" class="title-font mx-2 md:mx-auto my-5 md:w-md">
        <p class="text-center text-2xl font-bold">Medical Certificate</p>
        <p class="text-center mb-2">Digital certificate for a patient</p>
        <div class="bg-[#D9D9D9] p-4 rounded-lg mb-2">
        <form action="">
          <div>
            <p class="font-bold">Patient Information</p>
          <div class="flex justify-between items-center gap-2">
            <div>
              <label for="name">Name:</label>
              <ion-input id="name" name="name" placeholder="Full name"></ion-input>
            </div>
            <div>
              <label for="age" class="mt-2">Age:</label>
              <ion-input id="age" name="age" type="number" placeholder="Age"></ion-input>
            </div>
          </div>

          <div class="flex justify-between items-center gap-2">
            <div>
              <label for="gender" class="mt-2">Gender:</label>
              <ion-input id="gender" name="gender" placeholder="Gender"></ion-input>
            </div>
            <div>
              <label for="address" class="mt-2">Date Issued:</label>
              <ion-input id="address" name="address" type="date"></ion-input>
            </div>
          </div>
           <div>
            <label for="address" class="mt-2">Address:</label>
            <ion-input id="address" name="address" placeholder="Address"></ion-input>
           </div>
          </div>

          <div class="mt-2">
            <p class="font-bold">Clinical Information</p>
           <div>
            <label for="address" class="mt-2">Impression:</label>
            <ion-input id="address" name="address" placeholder="Describe the patient’s clinical findings..."></ion-input>
           </div>
           <div>
            <label for="address" class="mt-2">Remarks:</label>
            <ion-input id="address" name="address" placeholder="Regard with attention..."></ion-input>
           </div>
          </div>
          
        </form>
        </div>
        
            <div class="flex justify-end mt-3">
              <ion-button fill="clear" class="rounded-sm border border-black hover:bg-white hover:text-[#023E8A] transition duration-300 ease-in-out text-sm bg-[#023E8A] text-white normal-case">
                Generate Prescription
              </ion-button>
            </div>
      </div>
    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">
import { IonPage, IonHeader, IonToolbar, IonTitle, IonContent } from '@ionic/vue';
import ExploreContainer from '@/components/ExploreContainer.vue';
import Header from '@/components/Header.vue';
</script>

<style scoped>
ion-page, ion-header, ion-toolbar, ion-content {
    --background: #F0F0F0;
    --color: #000000;
}
#form-container{
    background-color: white;
    padding: 10px 20px;
}
ion-input{
    --background: white;
    --border-radius: 2px;
    --padding-start: 10px;
    --padding-end: 10px;
}
</style>
