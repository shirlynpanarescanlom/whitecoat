<template>
  <ion-page>
    <ion-tabs>
      <ion-router-outlet></ion-router-outlet>
      <ion-tab-bar slot="bottom">
        <ion-tab-button tab="tab1" href="/tabs/tab1">
          <font-awesome-icon :icon="[ 'fas', 'home' ]" class="text-4xl md:text-2xl" />
        </ion-tab-button>

        <ion-tab-button tab="tab2" href="/tabs/tab2">
          <font-awesome-icon :icon="[ 'fas', 'prescription' ]" class="text-4xl md:text-2xl" />
        </ion-tab-button>

        <ion-tab-button tab="tab3" href="/tabs/tab3">
          <font-awesome-icon :icon="[ 'fas', 'file-lines' ]" class="text-4xl md:text-2xl" />
        </ion-tab-button>

        <ion-tab-button tab="tab3" href="/tabs/tab3">
          <font-awesome-icon :icon="[ 'fas', 'gear' ]" class="text-4xl md:text-2xl" />
        </ion-tab-button>
      </ion-tab-bar>
    </ion-tabs>
  </ion-page>
</template>

<script setup lang="ts">
import { IonTabBar, IonTabButton, IonTabs, IonLabel, IonIcon, IonPage, IonRouterOutlet } from '@ionic/vue';
</script>

<style scoped>
ion-tab-bar {
  --ion-background-color: #023E8A;
}
</style>
