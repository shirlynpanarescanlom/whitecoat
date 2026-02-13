<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <Header />
      </ion-toolbar>
    </ion-header>

    <ion-content :fullscreen="true">
      <div class="bg-white rounded-lg my-4 mx-3 md:mx-auto md:w-md">
        <div class="bg-[#D9D9D9] p-2 rounded-t-lg mb-2 font-bold text-lg">
          <p>Doctor's Information</p>
        </div>

        <div class="px-2">
          <ion-label>Username:</ion-label>
          <ion-input
            v-model="doctor.username"
            :disabled="!isEditing"
            class="bg-[#D9D9D9] rounded-md p-2"
          />
        </div>

        <div class="px-2">
          <ion-label>Email</ion-label>
          <ion-input
            v-model="doctor.email"
            :disabled="!isEditing"
            class="bg-[#D9D9D9] rounded-md p-2"
          />
        </div>

        <div class="px-2 pb-2">
          <ion-label>Password</ion-label>
          <ion-input
            type="password"
            v-model="doctor.password"
            :disabled="!isEditing"
            class="bg-[#D9D9D9] rounded-md p-2"
          >
            <ion-input-password-toggle style="--color: black;" slot="end" />
          </ion-input>
        </div>

        <!-- File Attachment -->
        <div class="px-2 pb-4">
          <ion-label>Prescription</ion-label>

          <div v-if="doctor.presciptionFileName" class="flex items-center gap-2 mt-2">
            <span class="text-sm text-blue-600 underline cursor-pointer" @click="viewFile('prescription')">
              {{ doctor.presciptionFileName }}
            </span>
          </div>

          <input
            v-if="isEditing"
            type="file"
            @change="handlePrescriptionUpload"
            class="mt-2 text-sm"
          />
        </div>

        <div class="px-2 pb-4">
          <ion-label>Medical Certificate</ion-label>

          <div v-if="doctor.medcertFileName" class="flex items-center gap-2 mt-2">
            <span class="text-sm text-blue-600 underline cursor-pointer" @click="viewFile('medical')">
              {{ doctor.medcertFileName }}
            </span>
          </div>

          <input
            v-if="isEditing"
            type="file"
            @change="handleMedicalCertificateUpload"
            class="mt-2 text-sm"
          />
        </div>
      </div>

      <!-- Buttons -->
      <div class="my-4 mx-3 md:mx-auto flex justify-between items-center md:w-md gap-2">
        <ion-button
          fill="clear"
          @click="enableEdit"
          class="w-full mb-4 border border-black font-bold text-sm rounded-lg hover:bg-[#023E8A] hover:text-white text-[#023E8A]"
        >
          Edit
        </ion-button>

        <ion-button
          fill="clear"
          @click="updateDoctor"
          class="w-full mb-4 border font-bold text-sm bg-[#023E8A] text-white rounded-lg hover:bg-white hover:text-[#023E8A] hover:border-black"
        >
          Update
        </ion-button>
      </div>
    </ion-content>
  </ion-page>
</template>

<script lang="ts">
import { reactive, ref } from "vue";
import { IonPage, IonHeader, IonToolbar, IonContent } from "@ionic/vue";
import Header from "@/components/Header.vue";

export default {
  name: "DoctorInfoPage",

  components: {
    IonPage,
    IonHeader,
    IonToolbar,
    IonContent,
    Header,
  },

  setup() {
    const doctor = reactive({
      username: "drjohn123",
      email: "drjohn@example.com",
      password: "password123",
      prescriptionFile: null as File | null,
      medicalCertificateFile: null as File | null,
      presciptionFileName: "Rx.docx",
      medcertFileName: "SampleMedicalCertPX.docx",
    });

    const isEditing = ref(false);

    const enableEdit = () => {
      isEditing.value = true;
    };

    const handlePrescriptionUpload = (event: Event) => {
      const target = event.target as HTMLInputElement;
      if (target.files && target.files[0]) {
        doctor.prescriptionFile = target.files[0];
        doctor.presciptionFileName = target.files[0].name;
      }
    };

    const handleMedicalCertificateUpload = (event: Event) => {
      const target = event.target as HTMLInputElement;
      if (target.files && target.files[0]) {
        doctor.medicalCertificateFile = target.files[0];
        doctor.medcertFileName = target.files[0].name;
      }
    };

    const viewFile = (type: "prescription" | "medical") => {
      const fileToOpen =
        type === "prescription"
          ? doctor.prescriptionFile
          : doctor.medicalCertificateFile;

      if (fileToOpen) {
        const fileURL = URL.createObjectURL(fileToOpen);
        window.open(fileURL, "_blank");
      } else {
        alert("No file uploaded yet.");
      }
    };

    const updateDoctor = () => {
      console.log("Updated Doctor Info:", doctor);
      alert("Doctor information updated successfully!");
      isEditing.value = false;
    };

    return {
      doctor,
      isEditing,
      enableEdit,
      handlePrescriptionUpload,
      handleMedicalCertificateUpload,
      viewFile,
      updateDoctor,
    };
  },
};
</script>

<style scoped>
ion-page,
ion-header,
ion-toolbar,
ion-content {
  --background: #f0f0f0;
  --color: #000000;
}

ion-input {
  --padding-start: 8px;
  --padding-end: 8px;
  --border-color: transparent;
  --highlight-color: none;
}
</style>
