<template>
      <!-- --------------- MODAL --------------- -->
      <ion-modal :is-open="isOpen" @didDismiss="closeModal">
        <div class="flex flex-col justify-center items-center margin-auto">
          <div class="modal-header w-full flex justify-end p-2">
            <font-awesome-icon name="xmark" :icon="['fas', 'xmark']" class="text-black text-xl" @click="closeModal"></font-awesome-icon>
          </div>

          <div class="preview-area bg-[#D9D9D9] w-md" ref="previewRef">
            <!-- Render a simple preview -->
            <div class="prescription-preview">
              <h3>Prescription</h3>
              <p><b>Name:</b> {{ form.name }}</p>
              <p><b>Age:</b> {{ form.age }}</p>
              <p><b>Diagnosis:</b> {{ form.diagnosis }}</p>

              <div v-for="(med, i) in form.medications" :key="i">
                <hr />
                <p><b>Medication {{ i + 1 }}:</b> {{ med.name }}</p>
                <p><b>Dosage:</b> {{ med.dosage }}</p>
                <p><b>Frequency:</b> {{ med.frequency }}</p>
              </div>
            </div>
          </div>

          <div class="w-md flex items-center justify-between mt-4">
            <ion-button fill="clear" @click="previewOnly">
              <ion-icon name="eye-outline"></ion-icon>
              Preview Prescription
            </ion-button>

            <ion-button fill="clear" @click="printPrescription">
              <ion-icon name="print-outline"></ion-icon>
              Print
            </ion-button>

            <ion-button fill="clear" @click="exportPDF">
              <ion-icon name="document-outline"></ion-icon>
              Export as PDF
            </ion-button>
          </div>
          </div>
      </ion-modal>
</template>

<script lang="ts">
import { defineComponent, ref } from "vue";
import { IonIcon } from "@ionic/vue";
import html2canvas from "html2canvas";
import jsPDF from "jspdf";

export default defineComponent({
  name: "PrescriptionModal",

  props: {
    form: {
      type: Object,
      required: true
    },
    isOpen: {
      type: Boolean,
      required: true
    }
  },

  emits: ["close"],

  setup(props, { emit }) {
    const previewRef = ref<HTMLElement | null>(null);

    const closeModal = () => {
      emit("close");
    };

    const previewOnly = () => {
      alert("Preview shown above!");
    };

    const printPrescription = () => {
      window.print();
    };

    const exportPDF = async () => {
      if (!previewRef.value) return;

      const canvas = await html2canvas(previewRef.value);
      const imgData = canvas.toDataURL("image/png");

      const pdf = new jsPDF("p", "mm", "a4");
      pdf.addImage(imgData, "PNG", 10, 10, 190, 0);
      pdf.save("prescription.pdf");
    };

    return {
      previewRef,
      closeModal,
      previewOnly,
      printPrescription,
      exportPDF
    };
  }
});
</script>


<style scoped>
ion-modal{
    --background: #FFFFFF;
}
.modal-header{
  display:flex;
  justify-content:flex-end;
}

.preview-area{
  background:white;
  border-radius: 8px;
  border: 1px solid black;
}

</style>
