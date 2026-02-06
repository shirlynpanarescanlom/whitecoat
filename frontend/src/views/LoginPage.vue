<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <div class="flex justify-between px-4 py-2">
        <img src="../assets/logo/deped.png" alt="Logo" class="h-20 w-30">
        <img src="../assets/logo/division.png" alt="Logo" class="h-20 w-20">
      </div>
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
            <ion-input
              class="custom-input mx-auto h-15 shadow bg-white rounded-full border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
              id="username"
              type="text"
              placeholder="Enter your username"
            />
            <label class="block text-gray-700 text-lg font-bold mb-2 mt-1" for="username">
              Username
            </label>
          </div>
          <div class="mb-6">
            <ion-input
              class="custom-input mx-auto h-15 shadow bg-white rounded-full border rounded w-full py-2 px-3 text-gray-700 mb-3 leading-tight focus:outline-none focus:shadow-outline"
              id="password"
              placeholder="Enter your password">
              <ion-input-password-toggle style="--color: black;" slot="end"></ion-input-password-toggle>
              </ion-input>
            <label class="block text-gray-700 text-lg font-bold mb-2 mt-1" for="password">
              Password
            </label>
          </div>
          <div class="mx-auto text-center">
            <ion-button 
             fill="clear"
             class="p-2 font-bold text-xl text-[#0034B7] rounded-full mb-4 mx-auto border border-black font-bold hover:bg-[#0034B7] hover:text-white transition duration-300 ease-in-out"
             type="button"
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



</script>

<style scoped>
#archivo {
  font-family: 'Archivo Black', sans-serif;
}
.custom-input {
  --highlight-color: none;
  --padding-start: 10px;
  --padding-end: 10px;
  --color: black;
}
</style>