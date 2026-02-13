<template>
  <!-- --------------- MODAL --------------- -->
  <ion-modal :is-open="isOpen" @didDismiss="closeModal">
    <div class="flex flex-col h-full p-4">

      <!-- Close Button -->
      <div class="modal-header w-full flex justify-end mb-2">
        <font-awesome-icon 
          :icon="['fas', 'xmark']"
          class="text-black text-2xl cursor-pointer hover:text-gray-600" 
          @click="closeModal"
        />
      </div>

      <!-- ================= HIDDEN PRESCRIPTION (FOR IMAGE GENERATION) ================= -->
      <div
        v-if="form && form.name"
        ref="previewRef"
        style="position: absolute; left: -9999px; top: 0; width: 816px; height: 1056px; background: white; padding: 40px; font-family: 'Times New Roman', serif; box-sizing: border-box; border: 3px solid #000;"
      >
        <!-- Header Section -->
        <div style="text-align: center; margin-bottom: 30px;">
          <div style="display: flex; align-items: flex-start; justify-content: space-between; padding: 0 20px;">
            <!-- Left Logo - DepEd -->
            <div style="width: 80px; height: 80px; border: 2px solid #000; border-radius: 50%; display: flex; align-items: center; justify-content: center; flex-shrink: 0; background: #1a237e;">
              <div style="text-align: center; color: white; font-size: 10px; line-height: 1.2;">
                <div style="font-weight: bold;">DepEd</div>
                <div style="font-size: 8px;">DEPED</div>
              </div>
            </div>
            
            <!-- Center Text -->
            <div style="flex: 1; padding: 0 15px;">
              <h1 style="margin: 0 0 3px 0; font-size: 15px; font-weight: bold; color: #000;">Republic of the Philippines</h1>
              <h2 style="margin: 0 0 3px 0; font-size: 14px; font-weight: bold; color: #000;">Department of Education</h2>
              <p style="margin: 0 0 2px 0; font-size: 13px; font-weight: bold; color: #000;">Region VII - Central</p>
              <p style="margin: 0 0 2px 0; font-size: 13px; font-weight: bold; color: #000;">DIVISION OF LAPU-</p>
              <p style="margin: 0 0 2px 0; font-size: 13px; font-weight: bold; color: #000;">LAPU CITY</p>
              <p style="margin: 0 0 2px 0; font-size: 12px; font-weight: bold; color: #000;">B.M. Dimataga St.,</p>
              <p style="margin: 0; font-size: 12px; font-weight: bold; color: #000;">Lapu-Lapu City</p>
            </div>
            
            <!-- Right Logo - DOH -->
            <div style="width: 80px; height: 80px; border: 2px solid #000; border-radius: 50%; display: flex; align-items: center; justify-content: center; flex-shrink: 0; background: #ffd700;">
              <div style="text-align: center; color: #000; font-size: 10px; line-height: 1.2; font-weight: bold;">
                <div>DOH</div>
                <div style="font-size: 8px;">HEALTH</div>
              </div>
            </div>
          </div>
        </div>

        <!-- Patient Information -->
        <div style="margin-bottom: 30px; font-size: 13px; color: #000;">
          <div style="display: flex; justify-content: space-between; margin-bottom: 8px;">
            <div style="width: 48%;">
              <span style="font-weight: bold;">Name:</span>
              <span style="border-bottom: 2px solid #000; display: inline-block; width: 75%; padding-left: 5px;">{{ form.name }}</span>
            </div>
            <div style="width: 48%; text-align: left;">
              <span style="font-weight: bold;">Age/Sex:</span>
              <span style="border-bottom: 2px solid #000; display: inline-block; width: 60%; padding-left: 5px;">{{ form.age }}/{{ form.gender }}</span>
            </div>
          </div>
          <div style="display: flex; justify-content: space-between; margin-bottom: 8px;">
            <div style="width: 48%;">
              <span style="font-weight: bold;">Address:</span>
              <span style="border-bottom: 2px solid #000; display: inline-block; width: 70%; padding-left: 5px;">{{ form.address }}</span>
            </div>
            <div style="width: 48%; text-align: left;">
              <span style="font-weight: bold;">Date:</span>
              <span style="border-bottom: 2px solid #000; display: inline-block; width: 65%; padding-left: 5px;">{{ form.dateIssued }}</span>
            </div>
          </div>
        </div>

        <!-- Rx Symbol -->
        <div style="text-align: left; margin: 30px 0 20px 0;">
          <span style="font-size: 56px; font-weight: bold; font-style: italic; color: #000; font-family: 'Brush Script MT', cursive;">℞</span>
        </div>

        <!-- Diagnosis -->
        <div style="margin-bottom: 20px; font-size: 13px; color: #000;">
          <div style="font-weight: bold; margin-bottom: 8px;">DIAGNOSIS:</div>
          <div style="padding-left: 15px; line-height: 1.6;">
            {{ form.diagnosis }}
          </div>
        </div>

        <!-- Medications -->
        <div style="margin-bottom: 20px; font-size: 13px; color: #000; min-height: 300px;">
          <div style="font-weight: bold; margin-bottom: 10px;">MEDICATIONS:</div>
          <div
            v-for="(med, index) in form.medications"
            :key="index"
            style="padding-left: 15px; margin-bottom: 15px; line-height: 1.7;"
          >
            <div style="margin-bottom: 5px;">
              <strong>{{ index + 1 }}. {{ med.name }}</strong>
            </div>
            <div style="padding-left: 20px;">
              <div>Sig: {{ med.dosage }} - {{ med.frequency }}</div>
              <div>Duration: {{ med.duration }}</div>
              <div>{{ med.instructions }}</div>
            </div>
          </div>
        </div>

        <!-- Additional Notes -->
        <div v-if="form.notes" style="margin-bottom: 30px; font-size: 13px; color: #000;">
          <div style="font-weight: bold; margin-bottom: 8px;">NOTES:</div>
          <div style="padding-left: 15px; line-height: 1.6;">
            {{ form.notes }}
          </div>
        </div>

        <!-- Doctor Signature Section -->
        <div style="position: absolute; bottom: 50px; right: 80px; text-align: center; width: 300px;">
          <div style="border-top: 2px solid #000; padding-top: 5px; margin-bottom: 5px;"></div>
          <div style="font-size: 13px; color: #000; line-height: 1.4; font-weight: bold;">
            <div>Dr. Lynne Rose T. Amistad</div>
            <div style="font-size: 12px; font-weight: normal;">Medical Officer III</div>
            <div style="font-size: 12px; font-weight: normal;">License No.: 0145401</div>
            <div style="font-size: 12px; font-weight: normal;">PTR: 7408611</div>
          </div>
        </div>
      </div>
      <!-- ================= END HIDDEN PRESCRIPTION ================= -->


      <!-- ================= IMAGE PREVIEW AREA (CENTERED WITH SHADOW) ================= -->
      <div class="flex-1 flex items-center justify-center w-full overflow-hidden">
        <div 
          class="bg-gray-300 rounded-lg p-4 shadow-2xl max-w-[400px] w-full"
        >
          <div class="bg-white border-4 border-blue-500 rounded-md p-3 h-[500px] flex items-center justify-center overflow-hidden">
            <img
              v-if="generatedImage"
              :src="generatedImage"
              class="max-h-full max-w-full object-contain"
              alt="Prescription Preview"
            />

            <div v-else-if="isGenerating" class="text-gray-500 text-center">
              <div class="mb-2">Generating preview...</div>
              <div class="text-xs">Please wait</div>
            </div>

            <div v-else class="text-red-500 text-center p-4">
              <p class="mb-2">Preview not available</p>
              <button 
                @click="retryGeneration" 
                class="mt-2 px-4 py-2 bg-blue-500 text-white rounded text-xs"
              >
                Retry Generation
              </button>
            </div>
          </div>
        </div>
      </div>
      <!-- ================= END PREVIEW AREA ================= -->


      <!-- ACTION BUTTONS (BOTTOM ROW) -->
      <div class="flex items-center justify-center gap-6 mt-4 pb-2 w-full">

        <!-- Preview Prescription -->
        <div class="flex flex-col items-center cursor-pointer hover:opacity-70" @click="retryGeneration">
          <font-awesome-icon 
            :icon="['fas', 'eye']"
            class="text-black text-4xl mb-1"
          />
          <p class="text-xs text-black font-medium text-center leading-tight">Preview<br/>Prescription</p>
        </div>

        <!-- Print -->
        <div class="flex flex-col items-center cursor-pointer hover:opacity-70" @click="printPrescription">
          <font-awesome-icon 
            :icon="['fas', 'print']"
            class="text-black text-4xl mb-1"
          />
          <p class="text-xs text-black font-medium text-center">Print</p>
        </div>

        <!-- Export as PDF -->
        <div class="flex flex-col items-center cursor-pointer hover:opacity-70" @click="exportPDF">
          <font-awesome-icon 
            :icon="['fas', 'file-pdf']"
            class="text-red-600 text-4xl mb-1"
          />
          <p class="text-xs text-black font-medium text-center leading-tight">Export as<br/>PDF</p>
        </div>

        <!-- Edit -->
        <div class="flex flex-col items-center cursor-pointer hover:opacity-70" @click="closeModal">
          <font-awesome-icon 
            :icon="['fas', 'pen']"
            class="text-black text-4xl mb-1"
          />
          <p class="text-xs text-black font-medium text-center">Edit</p>
        </div>

      </div>

    </div>
  </ion-modal>
</template>

<script lang="ts">
import { defineComponent, ref, watch, nextTick, PropType } from "vue";
import { IonModal } from "@ionic/vue";
import html2canvas from "html2canvas";
import jsPDF from "jspdf";

interface Medication {
  name: string;
  dosage: string;
  frequency: string;
  duration: string;
  instructions: string;
}

interface PrescriptionForm {
  name: string;
  age: string;
  gender: string;
  dateIssued: string;
  address: string;
  diagnosis: string;
  notes: string;
  medications: Medication[];
}

export default defineComponent({
  name: "PrescriptionModal",
  components: {
    IonModal,
  },
  props: {
    form: {
      type: Object as PropType<PrescriptionForm>,
      required: false,
      default: () => ({
        name: "",
        age: "",
        gender: "",
        dateIssued: "",
        address: "",
        diagnosis: "",
        notes: "",
        medications: []
      })
    },
    isOpen: {
      type: Boolean,
      required: true,
      default: false
    }
  },

  emits: ["close"],

  setup(props, { emit }) {

    const previewRef = ref<HTMLElement | null>(null);
    const generatedImage = ref<string>("");
    const isGenerating = ref(false);

    const closeModal = () => {
      emit("close");
    };

    // Generate PNG when modal opens
    const generateImage = async () => {
      if (!props.form || !props.form.name) {
        console.error("Form data is not available");
        isGenerating.value = false;
        return;
      }

      isGenerating.value = true;
      generatedImage.value = "";
      
      console.log("=== Starting Image Generation ===");
      console.log("Form data:", props.form);
      
      // Wait for DOM to be ready
      await nextTick();
      await new Promise(resolve => setTimeout(resolve, 300));

      if (!previewRef.value) {
        console.error("ERROR: previewRef is null");
        isGenerating.value = false;
        return;
      }

      console.log("Preview element found:", previewRef.value);

      try {
        const canvas = await html2canvas(previewRef.value, {
          scale: 2,
          useCORS: true,
          backgroundColor: '#ffffff',
          logging: false,
          allowTaint: false,
          width: 816,
          height: 1056
        });

        console.log("Canvas created successfully:", canvas.width, "x", canvas.height);

        const dataUrl = canvas.toDataURL("image/png");
        generatedImage.value = dataUrl;
        
        console.log("✓ Image generated successfully");
      } catch (error) {
        console.error("✗ Error generating image:", error);
      } finally {
        isGenerating.value = false;
      }
    };

    const retryGeneration = () => {
      console.log("Manual retry triggered");
      generateImage();
    };

    watch(
      () => props.isOpen,
      async (val) => {
        if (val) {
          console.log("=== Modal Opened ===");
          console.log("Received form data:", props.form);
          
          // Reset state
          generatedImage.value = "";
          isGenerating.value = false;
          
          // Wait for modal animation
          await nextTick();
          setTimeout(() => {
            generateImage();
          }, 700);
        } else {
          console.log("Modal closed");
        }
      }
    );

    const printPrescription = () => {
      if (!generatedImage.value) {
        alert("Please wait for the preview to generate first");
        return;
      }

      const win = window.open("", "_blank");
      if (!win) {
        alert("Please allow pop-ups to print");
        return;
      }

      const htmlContent = 
        '<!DOCTYPE html>' +
        '<html>' +
        '<head><title>Print Prescription</title>' +
        '<style>body { margin: 0; padding: 20px; text-align: center; } img { max-width: 100%; height: auto; }</style>' +
        '</head>' +
        '<body>' +
        '<img src="' + generatedImage.value + '" alt="Prescription" />' +
        '</body>' +
        '</html>';

      win.document.write(htmlContent);
      win.document.close();
      
      setTimeout(() => {
        win.print();
      }, 500);
    };

    const exportPDF = () => {
      if (!generatedImage.value) {
        alert("Please wait for the preview to generate first");
        return;
      }

      try {
        const pdf = new jsPDF("p", "mm", "a4");
        const imgWidth = 210;
        const imgHeight = 297;
        pdf.addImage(generatedImage.value, "PNG", 0, 0, imgWidth, imgHeight);
        pdf.save("prescription.pdf");
        console.log("PDF exported successfully");
      } catch (error) {
        console.error("Error exporting PDF:", error);
        alert("Failed to export PDF");
      }
    };

    return {
      previewRef,
      generatedImage,
      isGenerating,
      closeModal,
      printPrescription,
      exportPDF,
      retryGeneration
    };
  }
});
</script>

<style scoped>
ion-modal {
  --background: #FFFFFF;
  --height: 90vh;
  --width: 90vw;
  --max-width: 600px;
  --border-radius: 10px;
}

.modal-header {
  display: flex;
  justify-content: flex-end;
}
</style>