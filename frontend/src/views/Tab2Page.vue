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
                  <ion-input v-model="form.name" id="name" name="name" placeholder="Full name"></ion-input>
                </div>

                <div class="w-full">
                  <label for="age" class="mt-2">Age:</label>
                  <ion-input v-model="form.age" id="age" name="age" type="number" placeholder="Age"></ion-input>
                </div>
              </div>

              <div class="flex justify-between items-center gap-2">
                <div class="w-full">
                  <label for="gender" class="mt-2">Gender:</label>
                  <ion-input v-model="form.gender" id="gender" name="gender" placeholder="Gender"></ion-input>
                </div>

                <div class="w-full">
                  <label for="address" class="mt-2">Date Issued:</label>
                  <ion-input v-model="form.dateIssued" id="address" name="address" type="date"></ion-input>
                </div>
              </div>

              <div>
                <label for="address" class="mt-2">Address:</label>
                <ion-input v-model="form.address" id="address" name="address" placeholder="Address"></ion-input>
              </div>

              <div>
                <label for="address" class="mt-2">Diagnosis:</label>
                <ion-input v-model="form.diagnosis" id="address" name="address" placeholder="Describe the patient’s diagnosis:s..."></ion-input>
              </div>

              <div>
                <label for="address" class="mt-2">Additional Notes:</label>
                <ion-input v-model="form.notes" id="address" name="address" placeholder="Any follow-up information..."></ion-input>
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
                  <!-- Add Medication -->
                  <ion-button
                    fill="clear"
                    class="font-bold mb-4 border border-black hover:bg-white transition duration-300 ease-in-out text-sm text-gray-600 rounded-lg normal-case flex items-center gap-2"
                    @click.prevent="addMedication"
                  >
                    <font-awesome-icon :icon="['fas', 'plus']" class="text-lg mr-2 text-gray-600 cursor-pointer align-middle"/>
                    Add Prescription
                  </ion-button>
                </div>
              </div>

              <!-- Medication List -->
              <div
                v-for="(med, index) in form.medications"
                :key="index"
                class="border border-black rounded-lg p-2 gap-2 mb-2"
              >
                <div class="flex justify-between items-center">
                  <p class="font-bold">Medication {{ index + 1 }}</p>
                  <ion-button
                    fill="clear"
                    color="danger"
                    class="font-bold mb-2 border border-black hover:bg-white transition duration-300 ease-in-out text-sm text-gray-600 rounded-lg normal-case"
                    @click.prevent="removeMedication(index)"
                  >
                    Remove
                  </ion-button>
                </div>

                <div>
                  <label for="name">Medication Name:</label>
                  <ion-input v-model="med.name" id="name" name="name" placeholder="e.g., Amoxicillin 500mg"></ion-input>
                </div>

                <div class="flex justify-between items-center gap-2">
                  <div>
                    <label for="name">Dosage:</label>
                    <ion-input v-model="med.dosage" id="name" name="name" placeholder="e.g., 1 tablet"></ion-input>
                  </div>

                  <div>
                    <label for="age" class="mt-2">Frequency:</label>
                    <ion-input v-model="med.frequency" id="age" name="age" type="number" placeholder="e.g., Twice daily"></ion-input>
                  </div>
                </div>

                <div>
                  <label for="address" class="mt-2">Duration:</label>
                  <ion-input v-model="med.duration" id="address" name="address" placeholder="e.g., 7 days"></ion-input>
                </div>

                <div>
                  <label for="address" class="mt-2">Instructions:</label>
                  <ion-input v-model="med.instructions" id="address" name="address" placeholder="e.g., After meal, take with water"></ion-input>
                </div>
              </div>

            </div>
          </form>
        </div>

        <div class="flex justify-end mt-3">
          <ion-button
            fill="clear"
            class="font-bold rounded-sm border border-black hover:bg-white hover:text-[#023E8A] transition duration-300 ease-in-out text-sm bg-[#023E8A] text-white normal-case"
            @click="generatePrescription"
          >
            Generate Prescription
          </ion-button>
        </div>
      </div>

        <!-- --------------- MODAL --------------- -->
        <PrescriptionModal :form="form" :isOpen="showModal" @close="showModal = false"/>
        <!-- --------------- END MODAL --------------- -->
    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">
import { ref } from "vue";
import { IonPage, IonHeader, IonToolbar, IonContent } from "@ionic/vue";
import Header from "../components/Header.vue";
import  PrescriptionModal from "../components/PrescriptionModal.vue";

const showModal = ref(false);
const form = ref({
  name: "",
  age: "",
  gender: "",
  dateIssued: "",
  address: "",
  diagnosis: "",
  notes: "",
  medications: [
    {
      name: "",
      dosage: "",
      frequency: "",
      duration: "",
      instructions: "",
    },
  ],
});

const addMedication = () => {
  form.value.medications.push({
    name: "",
    dosage: "",
    frequency: "",
    duration: "",
    instructions: "",
  });
};

const removeMedication = (index: number) => {
  form.value.medications.splice(index, 1);
};

const generatePrescription = () => {
  console.log("Prescription Data:", form.value);
  showModal.value = true;

};
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
