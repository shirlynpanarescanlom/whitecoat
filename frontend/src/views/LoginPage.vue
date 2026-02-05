<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <Header/>
      </ion-toolbar>
    </ion-header>
    <ion-content class="ion-padding-bottom">
        <div class="pb-32">
            <div class="mt-8">
                <img src="../assets/logo/doctors.png" alt="doctors" class="h-40 w-60 mx-auto rounded-full"/>
                <p id="archivo" class="text-center font-bold text-3xl mt-2 mb-4">WhiteCoat</p>
            </div>

      <div class="bg-[#D9D9D9] mx-8 md:mx-auto p-6 rounded-4xl width-full md:w-sm items-center">
        <p class="text-5xl font-bold mb-5 mt-2 text-center">LOG IN</p>
        <form class="w-full">
          <div class="mb-4">
            <input
              class="mx-auto h-15 shadow bg-white rounded-full border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
              id="username"
              type="text"
              placeholder="Enter your username"
            />
            <label class="block text-gray-700 text-lg font-bold mb-2 mt-1" for="username">
              Username
            </label>
          </div>
          <div class="mb-6">
            <input
              class="mx-auto h-15 shadow bg-white rounded-full border rounded w-full py-2 px-3 text-gray-700 mb-3 leading-tight focus:outline-none focus:shadow-outline"
              id="password"
              type="password"
              placeholder="Enter your password"
            />
            <label class="block text-gray-700 text-lg font-bold mb-2 mt-1" for="password">
              Password
            </label>
          </div>
          <div class="mx-auto text-center">
            <ion-button 
             fill="clear"
            class="w-30 rounded-full mb-4 mx-auto border border-black font-bold"
            >
              Sign In
            </ion-button>
          </div>
        </form>
      </div>
    </div>
    </ion-content>
  </ion-page>
  </template>


<script setup lang="ts">
import Header from '@/components/Header.vue';



</script>

<style scoped>
#archivo {
  font-family: 'Archivo Black', sans-serif;
}
</style>