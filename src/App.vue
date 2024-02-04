<script setup>
import GraficoDona from "./components/GraficoDona.vue";
import GraficoBarra from "./components/GraficoBarra.vue";
import GraficoDona2 from "./components/GraficoDona2.vue";
import GraficoLinea from "./components/GraficoLinea.vue";
import GraficoLinea2 from "./components/GraficoLinea2.vue";
import GraficoProgreso from "./components/GraficoProgreso.vue";
import Slider from "./components/Slider.vue";
import Navbar from "./components/Navbar.vue";
import Breadcrumb from "./components/Breadcrumb.vue";
</script>

<template>
  <Navbar />
  <Breadcrumb />

  <div class="m-4 grid grid-cols-1 gap-4 sm:grid-cols-4">
    <div
      class="h-72 flex-col rounded-lg bg-gray-700 sm:col-span-2 sm:row-span-2"
    >
      <div class="m-4 flex text-white">
        <p>Best selling</p>
        <p class="ml-auto text-gray-400">This week</p>
        <!-- Icono flecha abajo -->
        <svg
          xmlns="http://www.w3.org/2000/svg"
          height="1.2em"
          viewBox="0 0 320 512"
          fill="currentColor"
          class="ml-2 text-gray-400"
        >
          <!--! Font Awesome Free 6.4.0 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2023 Fonticons, Inc. -->
          <path
            d="M182.6 470.6c-12.5 12.5-32.8 12.5-45.3 0l-128-128c-9.2-9.2-11.9-22.9-6.9-34.9s16.6-19.8 29.6-19.8H288c12.9 0 24.6 7.8 29.6 19.8s2.2 25.7-6.9 34.9l-128 128z"
          />
        </svg>
      </div>
      <div class="m-3 mx-6 flex rounded-lg bg-tarjetas p-1 px-3 text-white">
        <p>Tuesday</p>
        <p class="ml-auto">215.523 pcs</p>
      </div>
      <div class="flex items-center justify-center">
        <div class="w-52 p-2">
          <GraficoDona2 />
        </div>
        <div class="hidden w-64 md:block">
          <GraficoBarra />
        </div>
      </div>
    </div>

    <div class="h-36 rounded-lg bg-gray-700 sm:col-start-1 sm:row-start-3">
      <GraficoProgreso />
    </div>
    <div
      class="flex h-36 justify-center rounded-lg bg-gray-700 sm:col-start-2 sm:row-start-3"
    >
      <GraficoLinea2 />
    </div>
    <div
      class="h-36 flex-col justify-center rounded-lg bg-gray-700 p-4 sm:col-start-1 sm:row-start-4"
    >
      <div class="flex">
        <p class="font-bold text-white">$456,623</p>
        <p class="ml-auto text-gray-400">Monthly</p>
        <!-- Icono flecha abajo -->
        <svg
          xmlns="http://www.w3.org/2000/svg"
          height="1.2em"
          viewBox="0 0 320 512"
          fill="currentColor"
          class="ml-2 text-gray-400"
        >
          <!--! Font Awesome Free 6.4.0 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2023 Fonticons, Inc. -->
          <path
            d="M182.6 470.6c-12.5 12.5-32.8 12.5-45.3 0l-128-128c-9.2-9.2-11.9-22.9-6.9-34.9s16.6-19.8 29.6-19.8H288c12.9 0 24.6 7.8 29.6 19.8s2.2 25.7-6.9 34.9l-128 128z"
          />
        </svg>
      </div>
      <GraficoLinea class="p-2" />
    </div>
    <div
      class="flex h-36 justify-center rounded-lg bg-gray-700 sm:col-start-2 sm:row-start-4"
    >
      <GraficoDona />
    </div>
    <div
      class="flex h-52 justify-center rounded-lg bg-gradient-to-r from-teal-400 to-teal-700 sm:col-span-2 sm:col-start-3 sm:row-start-1"
    >
      <GraficoBarra />
    </div>
    <div
      class="h-36 rounded-lg sm:col-span-2 sm:col-start-3 sm:row-span-3 sm:row-start-2"
    >
      <h1 class="mb-2 text-xl font-semibold text-white">Event Galleries</h1>
      <Slider class="mb-4" />
    </div>
  </div>
</template>

<style></style>
