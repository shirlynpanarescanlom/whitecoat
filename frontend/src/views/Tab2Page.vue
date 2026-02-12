<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <Header/>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true">
      <div id="form-container" class="px-2 py-4 md:mx-auto mx-2 title-font my-5 md:w-md">
        <p class="text-center text-2xl font-bold">Prescription</p>
        <p class="text-center mb-2">Digital prescription for a patient</p>
        <div class="bg-[#D9D9D9] p-4 rounded-lg mb-2">
        <form action="">
          <div>
            <p class="font-bold">Patient Information</p>
          <div class="flex justify-between items-center gap-2">
            <div class="w-full">
              <label for="name">Name:</label>
              <ion-input id="name" name="name" placeholder="Full name"></ion-input>
            </div>
            <div class="w-full">
              <label for="age" class="mt-2">Age:</label>
              <ion-input id="age" name="age" type="number" placeholder="Age"></ion-input>
            </div>
          </div>

          <div class="flex justify-between items-center gap-2">
            <div class="w-full">
              <label for="gender" class="mt-2">Gender:</label>
              <ion-input id="gender" name="gender" placeholder="Gender"></ion-input>
            </div>
            <div class="w-full">
              <label for="address" class="mt-2">Date Issued:</label>
              <ion-input id="address" name="address" type="date"></ion-input>
            </div>
          </div>
           <div>
            <label for="address" class="mt-2">Address:</label>
            <ion-input id="address" name="address" placeholder="Address"></ion-input>
           </div>
           <div>
            <label for="address" class="mt-2">Diagnosis:</label>
            <ion-input id="address" name="address" placeholder="Describe the patient’s diagnosis:s..."></ion-input>
           </div>
           <div>
            <label for="address" class="mt-2">Additional Notes:</label>
            <ion-input id="address" name="address" placeholder="Any follow-up information..."></ion-input>
           </div>
          </div>
       </form>
        </div>
        <div class="bg-[#D9D9D9] p-4 rounded-lg mb-2">
        <form action="">
          <div>
            <div class="flex justify-between items-center">
              <p class="font-bold">Medication</p>
              <div>
                <ion-button fill="clear" class="font-bold mb-4 border border-black hover:bg-white transition duration-300 ease-in-out text-sm text-gray-600 rounded-lg normal-case flex items-center gap-2">
                  <font-awesome-icon :icon="['fas', 'plus']" class="text-lg mr-2 text-gray-600 cursor-pointer align-middle"/>
                  Add Prescription
                </ion-button>
              </div>
            </div>
            <div class="border border-black rounded-lg p-2 gap-2">
              <p class="font-bold">Medication 1</p>
              <div>
                <label for="name">Medication Name:</label>
                <ion-input id="name" name="name" placeholder="e.g., Amoxicillin 500mg"></ion-input>
              </div>
              <div class="flex justify-between items-center gap-2">
              <div>
                <label for="name">Dosage:</label>
                <ion-input id="name" name="name" placeholder="e.g., 1 tablet"></ion-input>
              </div>
              <div>
                <label for="age" class="mt-2">Frequency:</label>
                <ion-input id="age" name="age" type="number" placeholder="e.g., Twice daily"></ion-input>
              </div>
            </div>

            <div>
              <label for="address" class="mt-2">Duration:</label>
              <ion-input id="address" name="address" placeholder="e.g., 7 days"></ion-input>
            </div>
            <div>
              <label for="address" class="mt-2">Instructions:</label>
              <ion-input id="address" name="address" placeholder="e.g., After meal, take with water"></ion-input>
            </div>
            </div>
            </div>
        </form>
            </div>
            <div class="flex justify-end mt-3">
              <ion-button fill="clear" class="font-bold rounded-sm border border-black hover:bg-white hover:text-[#023E8A] transition duration-300 ease-in-out text-sm bg-[#023E8A] text-white normal-case">
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
}
ion-input{
    --background: white;
    --border-radius: 2px;
    --padding-start: 10px;
    --padding-end: 10px;
    --highlight-color: none;
}
</style>
