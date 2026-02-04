<template>
    <ion-page>
    <ion-header>
      <ion-toolbar>
        <Header/>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true">
      <ion-header>
        <ion-toolbar>
          <ion-title size="large">Tab 2</ion-title>
        </ion-toolbar>
      </ion-header>

      <ExploreContainer name="Tab 2 page" />
    </ion-content>
  </ion-page>
</template>
<script lang="ts">
import ExploreContainer from "@/components/ExploreContainer.vue";
import Header from '@/components/Header.vue';
export default {
    
}
</script>