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

        <!-- ================= PATIENT INFO ================= -->
        <div class="bg-[#D9D9D9] p-4 rounded-lg mb-2">
          <form>
            <p class="font-bold">Patient Information</p>

            <div class="flex justify-between items-center gap-2">
              <div class="w-full">
                <label>Name:</label>
                <ion-input 
                  v-model="form.name" 
                  placeholder="Full name"
                  fill="solid"
                  class="custom-input"
                ></ion-input>
              </div>

              <div class="w-full">
                <label>Age:</label>
                <ion-input 
                  v-model="form.age" 
                  type="number" 
                  placeholder="Age"
                  fill="solid"
                  class="custom-input"
                ></ion-input>
              </div>
            </div>

            <div class="flex justify-between items-center gap-2">
              <div class="w-full">
                <label>Gender:</label>
                <ion-input 
                  v-model="form.gender" 
                  placeholder="Gender"
                  fill="solid"
                  class="custom-input"
                ></ion-input>
              </div>

              <div class="w-full">
                <label>Date Issued:</label>
                <ion-input 
                  v-model="form.dateIssued" 
                  type="date"
                  fill="solid"
                  class="custom-input"
                ></ion-input>
              </div>
            </div>

            <div>
              <label>Address:</label>
              <ion-input 
                v-model="form.address" 
                placeholder="Address"
                fill="solid"
                class="custom-input"
              ></ion-input>
            </div>

            <div>
              <label>Diagnosis:</label>
              <ion-input 
                v-model="form.diagnosis" 
                placeholder="Describe the patient's diagnosis..."
                fill="solid"
                class="custom-input"
              ></ion-input>
            </div>

            <div>
              <label>Additional Notes:</label>
              <ion-input 
                v-model="form.notes" 
                placeholder="Any follow-up information..."
                fill="solid"
                class="custom-input"
              ></ion-input>
            </div>
          </form>
        </div>

        <!-- ================= MEDICATION ================= -->
        <div class="bg-[#D9D9D9] p-4 rounded-lg mb-2">
          <form>
            <div class="flex justify-between items-center">
              <p class="font-bold">Medication</p>

              <ion-button
                fill="clear"
                class="font-bold mb-4 border border-black text-sm text-gray-600 rounded-lg normal-case"
                @click.prevent="addMedication"
              >
                Add Prescription
              </ion-button>
            </div>

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
                  class="font-bold mb-2 border border-black text-sm rounded-lg normal-case"
                  @click.prevent="removeMedication(index)"
                >
                  Remove
                </ion-button>
              </div>

              <div>
                <label>Medication Name:</label>
                <ion-input 
                  v-model="med.name" 
                  placeholder="e.g., Amoxicillin 500mg"
                  fill="solid"
                  class="custom-input"
                ></ion-input>
              </div>

              <div class="flex justify-between items-center gap-2">
                <div class="w-full">
                  <label>Dosage:</label>
                  <ion-input 
                    v-model="med.dosage" 
                    placeholder="e.g., 1 tablet"
                    fill="solid"
                    class="custom-input"
                  ></ion-input>
                </div>

                <div class="w-full">
                  <label>Frequency:</label>
                  <ion-input 
                    v-model="med.frequency" 
                    placeholder="e.g., Twice daily"
                    fill="solid"
                    class="custom-input"
                  ></ion-input>
                </div>
              </div>

              <div>
                <label>Duration:</label>
                <ion-input 
                  v-model="med.duration" 
                  placeholder="e.g., 7 days"
                  fill="solid"
                  class="custom-input"
                ></ion-input>
              </div>

              <div>
                <label>Instructions:</label>
                <ion-input 
                  v-model="med.instructions" 
                  placeholder="e.g., After meal"
                  fill="solid"
                  class="custom-input"
                ></ion-input>
              </div>
            </div>
          </form>
        </div>

        <!-- ================= ALERT ================= -->
        <div v-if="alertMessage" class="mb-2 text-red-600 font-semibold text-sm">
          {{ alertMessage }}
        </div>

        <!-- ================= GENERATE BUTTON ================= -->
        <div class="flex justify-end mt-3">
          <ion-button
            fill="clear"
            class="font-bold rounded-sm border border-black text-sm bg-[#023E8A] text-white normal-case"
            @click="generatePrescription"
          >
            Generate Prescription
          </ion-button>
        </div>
      </div>

      <!-- ================= MODAL ================= -->
      <PrescriptionModal
        :isOpen="showModal"
        :form="form"
        :docUrl="'https://yourdomain.com/prescription.docx'"
        @close="showModal = false"
      />
    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">
import { ref, computed, watch } from "vue";
import { IonPage, IonHeader, IonToolbar, IonContent, IonInput, IonButton } from "@ionic/vue";
import Header from "../components/Header.vue";
import PrescriptionModal from "../components/PrescriptionModal.vue";

const showModal = ref(false);
const alertMessage = ref(""); // store error message

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

/* ================= VALIDATION WITH ALERT ================= */
const isFormValid = computed(() => {
  const patientValid =
    form.value.name?.trim() !== "" &&
    form.value.gender?.trim() !== "" &&
    form.value.dateIssued !== "" &&
    form.value.address?.trim() !== "" &&
    form.value.diagnosis?.trim() !== "" &&
    form.value.age?.trim() !== "" &&
    !isNaN(Number(form.value.age)) &&
    Number(form.value.age) > 0;

  const medicationsValid =
    form.value.medications.length > 0 &&
    form.value.medications.every(
      (med) =>
        med.name?.trim() !== "" &&
        med.dosage?.trim() !== "" &&
        med.frequency?.trim() !== "" &&
        med.duration?.trim() !== "" &&
        med.instructions?.trim() !== ""
    );

  return patientValid && medicationsValid;
});

// Optional: Debugging
watch(isFormValid, (val) => {
  console.log("Form valid?", val, form.value);
});

const generatePrescription = () => {
  // Patient info validation
  if (form.value.name?.trim() === "") {
    alertMessage.value = "Please enter the patient's name.";
    return;
  }
  if (form.value.age?.trim() === "" || isNaN(Number(form.value.age)) || Number(form.value.age) <= 0) {
    alertMessage.value = "Please enter a valid age.";
    return;
  }
  if (form.value.gender?.trim() === "") {
    alertMessage.value = "Please enter the patient's gender.";
    return;
  }
  if (form.value.dateIssued === "") {
    alertMessage.value = "Please select the date issued.";
    return;
  }
  if (form.value.address?.trim() === "") {
    alertMessage.value = "Please enter the patient's address.";
    return;
  }
  if (form.value.diagnosis?.trim() === "") {
    alertMessage.value = "Please enter a diagnosis.";
    return;
  }

  // Medications validation
  for (let i = 0; i < form.value.medications.length; i++) {
    const med = form.value.medications[i];
    if (med.name?.trim() === "") {
      alertMessage.value = `Medication ${i + 1}: Please enter the medication name.`;
      return;
    }
    if (med.dosage?.trim() === "") {
      alertMessage.value = `Medication ${i + 1}: Please enter the dosage.`;
      return;
    }
    if (med.frequency?.trim() === "") {
      alertMessage.value = `Medication ${i + 1}: Please enter the frequency.`;
      return;
    }
    if (med.duration?.trim() === "") {
      alertMessage.value = `Medication ${i + 1}: Please enter the duration.`;
      return;
    }
    if (med.instructions?.trim() === "") {
      alertMessage.value = `Medication ${i + 1}: Please enter the instructions.`;
      return;
    }
  }

  // All good → reset alert & open modal
  alertMessage.value = "";
  console.log("Prescription Data:", form.value);
  showModal.value = true;
};
</script>

<style scoped>
ion-page, ion-header, ion-toolbar, ion-content {
  --background: #F0F0F0;
  --color: #000000;
}

#form-container {
  background-color: white;
}

ion-input {
  --background: white;
  --border-radius: 2px;
  --padding-start: 10px;
  --padding-end: 10px;
  margin-bottom: 8px;
}

ion-input.custom-input {
  --background: white;
}
</style>